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

Mettons maintenant du cache devant cette application. Le fichier suivant a été beaucoup pompé sur le net, principalement sur la doc de Sonata. Mon projet est en cours de développement, je n'ai donc pas passé beaucoup de temps à le fine-tuner.
Ainsi, je décline tout responsabilité sur les potentielles conneries écrites dans ce fichier : le but de l'article est de déplier toute la stack et de voir comment relier les différents composants. Les détails de configuration de varnish, je ne me suis pas encore penché dessus.

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

acl purge {
        "localhost";
}

#
# RECEIVE REQUEST FROM THE CLIENT
#
sub vcl_recv {

    set req.http.X-Forwarded-Port = "443";
    // Remove all cookies except the session ID.
    if (req.http.Cookie) {
        set req.http.Cookie = ";" + req.http.Cookie;
        set req.http.Cookie = regsuball(req.http.Cookie, "; +", ";");
        set req.http.Cookie = regsuball(req.http.Cookie, ";(PHPSESSID)=", "; \1=");
        set req.http.Cookie = regsuball(req.http.Cookie, ";[^ ][^;]*", "");
        set req.http.Cookie = regsuball(req.http.Cookie, "^[; ]+|[; ]+$", "");

        if (req.http.Cookie == "") {
            // If there are no more cookies, remove the header to get page cached.
            unset req.http.Cookie;
        }
    }

    if (req.method == "PURGE") {
        if (!client.ip ~ purge) {
            return(synth(405,"Not allowed."));
        }
        return (purge);
    }

    unset req.http.X-Forwarded-For;
    set req.http.X-Forwarded-For = client.ip;

    # Force lookup if the request is a no-cache request from the client
    if (req.http.Cache-Control ~ "no-cache") {
        return (pass);
    }

    if (req.http.Cookie) {
        # removes all cookies named __utm? (utma, utmb...) - tracking thing
        set req.http.Cookie = regsuball(req.http.Cookie, "(^|; ) *__utm.=[^;]+;? *", "\1");

        if (req.http.Cookie == "") {
            unset req.http.Cookie;
        }
    }

    ## Default request checks
    if (req.method != "GET" &&
        req.method != "HEAD" &&
        req.method != "PUT" &&
        req.method != "POST" &&
        req.method != "TRACE" &&
        req.method != "OPTIONS" &&
        req.method != "DELETE") {
            # Non-RFC2616 or CONNECT which is weird.
            return (pipe);
    }

    if (req.method != "GET" && req.method != "HEAD") {
        # We only deal with GET and HEAD by default
        return (pass);
    }

   ## Modified from default to allow caching if cookies are set, but not http auth
    if (req.http.Authorization) {
        /* Not cacheable by default */
        return (pass);
    }

    # Don't cache user/application area
    if (req.url ~ "(^/app.php|^/app_dev.php|^)/([a-z]{2})/(payment|order|booking|media|autocomplete|monitor).*") {
        return (pass);
    }

    # Don't cache admin area
    if (req.url ~ "(^/app.php|^/app_dev.php|^)/admin" || req.url ~ "(^/app.php|^/app_dev.php|^)/(([a-z]{2})/admin)") {
        return (pass);
    }

    # Don't cache security area
    if (req.url ~ "(^/app.php|^/app_dev.php|^)/(([a-z]{2}/|)(login|logout|login_check).*)") {
        return (pass);
    }

    ## Don't cache editor logged-in user sessions
    if (req.http.Cookie ~ "(sonata_page_is_editor)") {
        return (pass);
    }

    return (hash);
}


#
# RECEIVE RESPONSE FROM THE APPLICATION
#
sub vcl_backend_response
{
    # These status codes should always pass through and never cache.
    if (beresp.status == 404) {
        set beresp.http.X-Cache-Rule = "YES: but for 1m - beresp.status : " + beresp.status;
        set beresp.ttl = 1m;

        return (deliver);
    }

    if (beresp.status == 503 || beresp.status == 500) {
        set beresp.http.X-Cache-Rule = "NOT: beresp.status : " + beresp.status;
        set beresp.ttl = 0s;
        set beresp.uncacheable = true;

        return (deliver);
    }

    # Force the cache for the home
    if (bereq.url ~ "(^/app.php|^/app_dev.php|^)/([a-z]{2})(|/)$") {
        set beresp.ttl = 1m;
    }

    if (bereq.url ~ "\.(jpg|jpeg|gif|png|ico|css|zip|tgz|gz|rar|bz2|pdf|txt|tar|wav|bmp|rtf|js|flv|swf|html|htm|mov|avi|mp3|mpg)$") {
        unset beresp.http.set-cookie;
        set beresp.http.X-Cache-Rule = "YES: static files";
        set beresp.ttl = 24h;
    }

    #if (obj.http.Set-Cookie) {
    #    set obj.http.X-Cache-Rule = "NO: !obj.Set-Cookie";
    #    return (hit_for_pass);
    #}

    # No cache for Sonata Editor
    if (bereq.http.Cookie ~ "sonata_page_is_editor") {
        set beresp.ttl = 0s;
        set beresp.http.X-Cache-Rule = "NO: user has ROLE_SONATA_PAGE_ADMIN_PAGE_EDIT";
    }

    if (!beresp.ttl > 0s) {
        set beresp.http.X-Cache-Rule = "NO: beresp.ttl == 0";
        set beresp.uncacheable = true;
        return (deliver);
    }

    # All tests passed, therefore item is cacheable
    set beresp.http.X-Cache-Rule = "YES with ttl: " + beresp.ttl;

    # remove cookies for cached response
    unset beresp.http.set-cookie;

    return (deliver);
}

sub vcl_deliver {
    # add cache hit data
    if (obj.hits > 0) {
        # if hit add hit count
        set resp.http.X-Cache = "HIT";
        set resp.http.X-Cache-Hits = obj.hits;
    } else {
        set resp.http.X-Cache = "MISS";
    }
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
