---
title: Une stack Nginx/Varnish/PHP-FPM pour avoir du http2 et du cache
categories:
    - Dev

---

J'héberge un site fait en Symfony2. Mes besoins :

* du HTTP2
* du SSL (ça vient avec HTTP2, cool)
* du cache HTTP

Mes outils :

* Nginx
* Varnish
* PHP-FPM

Bon, le besoin de cache est overkill pour mon projet, pour l'instant. Je fais tout ça pour m'amuser surtout.

Prenons notre souffle avec une photo de chaton avant d'enchainer les horribles fichiers de configuration :

![](/images/kitten_1.png){.img-responsive}

La chaîne va ressembler à ça :
```
Browser -> Nginx (HTTP2 + SSL) -> Varnish (cache HTTP) -> Nginx (fichiers statiques et interfaçage avec PHP) -> PHP-FPM
```

Pour mettre tout ça en place, je commence par la fin et j'évolue peu à peu vers le début de la chaîne.

## Nginx (PHP et fichiers statiques)

```
server {
    root /CHEMIN_DU_PROJET/web;

    listen 6969;

    set_real_ip_from   127.0.0.1;
    real_ip_header     X-Forwarded-For;
    real_ip_recursive on;

    location / {
        try_files $uri /app.php$is_args$args;
    }
    location ~ ^/app_preprod\.php(/|$) {
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param HTTPS off;
        internal;
    }

    error_log /var/log/nginx/NOM_DU_PROJET_app_error.log;
    access_log /var/log/nginx/NOM_DU_PROJET_app_access.log;
}
```

Avec ce paté, le site est accessible sur le serveur sur le port 6969

## Varnish

Mettons maintenant du cache devant cette application. Le fichier suivant est fortement tronqué par rapport à mon fichier de configuration réel. Il fait juste en sorte que ça marche à peu près. Je ne veux pas prendre la responsabilité de mettre un fichier de configuration varnish que je n'ai pas encore fine-tuné et qui peut contenir des erreurs. Le but de l'article est surtout de voir comment coller les différents composants entre eux.

```
vcl 4.0;

backend default {
    .host = "127.0.0.1";
    .port = "6969";
    .connect_timeout = 600s;
    .first_byte_timeout = 600s;
    .between_bytes_timeout = 600s;
    .max_connections = 250;
}

```

## Nginx (HTTP2 et SSL)

On arrive au plus intéressant/compliqué/chiant.

Pour la petite histoire, j'ai essayé de me passer de Nginx à ce niveau en utilisant Pound. Je me disais que ça serait plus léger. Au final, la communauté, la documentation et les sources d'informations étant beaucoup plus grandes chez Nginx, j'ai laissé tomber Pound, avec lequel j'avais du mal à régler ma configuration SSL.


```
server {
    listen 443 ssl http2;

    server_name URL_DU_SITE.COM;

    ssl_certificate /etc/nginx/ssl/CERTIFICAT_SSL.crt;
    ssl_certificate_key /etc/nginx/ssl/CLE_PRIVEE.key;
    include common/ssl.conf;

    location / {
        proxy_http_version 1.1; # Important : sinon, nginx cause en http 1.0 avec varnish, et ça chie dans la colle
        proxy_pass http://127.0.0.1:6081; # Le port de varnish. Adapter au besoin. Voir /etc/default/varnish
        proxy_set_header X-Real-IP  $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto https;
        proxy_set_header X-Forwarded-Port 443;
        proxy_set_header Host $host;
    }

    error_log /var/log/nginx/NOM_DU_PROJET_ssl_error.log;
    access_log /var/log/nginx/NOM_DU_PROJET_ssl_access.log;
}

```

le fichier ssl.conf est le suivant :

```
ssl_session_cache shared:SSL:50m;
ssl_session_timeout 5m;

ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_prefer_server_ciphers on;
ssl_ciphers 'ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:DES-CBC3-SHA:HIGH:!aNULL:!eNULL:!EXPORT:!CAMELLIA:!DES:!MD5:!PSK:!RC4';
ssl_dhparam /etc/nginx/ssl/dhparam.pem; # généré avec la commande : openssl dhparam -out /etc/nginx/ssl/dhparam.pem 2048

add_header Strict-Transport-Security "max-age=31536000; includeSubdomains;";
```

J'ai volontairement isolé la configuration ssl dans un fichier commun pour la réutiliser à l'identique sur d'autres sites : j'utilise du SNI avec nginx pour avoir plusieurs sites en https sur la même IP.

## Nginx (redirection HTTP -> HTTPS)

Un petit serveur en plus pour gérer les redirections :

```
server {
    listen         80;
    server_name URL_DU_SITE.com;
    return 307 https://$host$request_uri;

    error_log /var/log/nginx/NOM_DU_PROJET_redirection_error.log;
    access_log /var/log/nginx/NOM_DU_PROJET_redirection_access.log;
}

```

J'ai choisi de faire une redirection 307 pour rediriger à l'identique les requêtes POST... je pourrais changer d'avis là dessus, je sais pas trop.

Prochaine étape : benchmarker un peu tout ça en trifouillant les différents paramètres, surtout au niveau de la compression, laissée de côté pour l'instant.
