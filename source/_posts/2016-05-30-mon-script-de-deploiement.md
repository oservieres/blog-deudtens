---
title: Mon script de déploiement
tags:
    - Dev

---

Je maintiens/développe un site en PHP (Symfony 2). J'ai besoin de le déployer sur des serveurs de préproduction et production. Pour l'instant, il n'y a qu'un seul frontal. Il s'agît d'un projet personnel avec pour l'instant peu de contraintes. Mon besoin :

* minimiser les dépendances requises ;
* déployer à partir d'un serveur d'intégration continue (je ne fais pas confiance à mon PC perso et à mes fichiers pour lancer un déploiement depuis le local) ;
* effectuer toutes les opérations de préparation sur le serveur de CI pour livrer un "paquet" tout prêt (je ne veux pas installer d'outils sur ma prod et la charger avec ce genre d'opérations);
* pas de git sur le serveur cible.

<!--more-->

## Solutions envisagées

* [Capistrano](http://capistranorb.com/) : j'ai touché à Ruby, et je n'ai pas aimé. Et je trouve Capistrano trop compliqué/lourd pour mon besoin simple. Ça ne satisfait pas mon premier critère.
* [Deployer](http://deployer.org/) : c'est cool, c'est en PHP, mais au moment ou je m'y suis interessé, sa logique était d'effectuer toutes les opérations de compilation/génération sur le serveur cible. Je ne sais pas si ça a évolué depuis, mais ça ne me convient pas.
* [Deliver](https://github.com/gerhard/deliver) : un outil de déploiement en bash. Le rêve pour moi. Mais j'avoue que j'ai eu un peu la flemme de m'y plonger en profondeur pour l'instant.


## Ma solution

J'ai bêtement utilisé un script bash. Je trouve ça facile et clair (marre qu'on dise l'inverse !).

Ça donne ça :

```
function ssh_command
{
    ssh -i CHEMIN_CLE_SSH USER@SERVER $1
}

# 1.Install dependencies
curl -sS https://getcomposer.org/installer | php
php composer.phar install

# 2.Compile/generate stuff
php app/console cache:clear --env=prod
php app/console cache:warmup --env=prod
php app/console assetic:dump --env=prod
php app/console assets:install --env=prod
rm -rf app/logs/*

# 3.Prepare release directory
RELEASE_DIR="/home/USER/project/releases/$(date +%F-%X)"
ssh_command "mkdir -p ${DATE_WORKDIR}"

# 4.Send project
rsync -avz --exclude .git --exclude web/app_dev.php . USER@SERVER:${RELEASE_DIR}

# 5.Run database migrations
ssh_command "cd ${RELEASE_DIR} && php app/console doctrine:migrations:migrate --env=prod"

# 6.Enable new site
ssh_command "rm -rf  /home/USER/project/current"
ssh_command "ln -sf ${RELEASE_DIR} /home/USER/project/current"

# 7.Reload FPM
ssh_command "sudo /etc/init.d/php7.0-fpm reload"

```

Ce script est exécuté par Jenkins, après lancement des tests. C'est aussi lui qui gère quelle branche déployer, gràce à un paramètre en entrée de build.

Quelques commentaires :

* Il faut remplacer USER par le nom du projet, pour lequel j'ai créé un utilisateur particulier.
* Ce script est bêtement lancé directement sur mon serveur de CI, car par chance il a la même configuration PHP que la production. Sinon, je passerais par du Docker.
* Je ne versionne pas Composer (j'en connais qui le font) (1).
* Je vire les logs générés par la console symfony pour éviter de les envoyer sur la prod (2). D'un autre côté, je fais des `--exclude` lors du rsync pour ne pas envoyer certains fichiers (4). Je pourrais peut-être uniformiser les deux.
* Je veille à bien supprimer le lien symbolique avant d'en créer un nouveau (6). Je ne sais plus pourquoi, l'option `-f` de ln ne suffit pas.
* Je recharge FPM (7) car sans ça, le serveur ne capte pas que le changement de lien symbolique a fait changer les sources du site.

Bref, je suis conscient de la cratitude un peu borderline de certains aspects de ce script, mais il suffit amplement à répondre à mes attentes. Pas besoin d'over-engineerer. Il peut évoluer avec le temps, ou bien être remplacé par autre chose plus tard. En l'état, il m'a demandé 30 minutes de développement, ce que j'estime très rentable.

## Et après ?

Peut-être remplacer ce script par [PHPloy](http://blog.epoc.fr/2016/05/27/deployer-simplement-ses-projets-avec-phploy/), qui a l'air très cool. Sa méthode de calcul de delta au niveau des sources à déployer a l'air très rigolote.

Il manque dans mon script de quoi gérer des fichiers "shared" : des fichiers qui restent persistants release après release. Facile à gérer : faites un répertoire à côté qui les contient, et créez des liens symboliques à chaque déploiement. C'est ce que je fais, mais je ne l'ai pas mis dans l'extrait de script car je l'ai fait mochement, j'assume pas.

Lorsque j'aurai plusieurs frontaux sur lesquels déployer, je n'aurai qu'à rajouter une boucle sur mes différents serveurs, sauf pour l'étape de migration de base de données.
