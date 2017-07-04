---
title: Check-list de mise en production
tags:
    - Dev

---

![](/images/deploy-meme.jpeg){.img-responsive}
i
Je parlais il y a peu de [déployer en production le plus tôt possible](). Aujourd'hui, je m'attarde sur ce qui constitue une mise en production initiale d'un site web.

<!--more-->

Le but de la liste qui suit est de référencer tous les machins qu'il faut faire lors d'une mise en production. Parmi ces trucs, j'ai oublié d'en faire certains. Parmi ces trucs oubliés, une partie attend toujours d'être réalisée.

Certains de ces points peuvent paraitre évidents, voir automatiques ou non pertinents selon votre environnement et vos choix.

##Nom de domaine

* Configurer une alerte sur l'expiration du nom de domaine.
* Configurer une alerte sur l'expiration du certificat SSL.

##Backup

* Vérifier que les backups des contenus générés/uploadés et de la base de donnée sont faits.
* Vérifier que les backups sont bien récupérables et applicables.
* Vérifier que les backups sont régulièrement nettoyés

##Monitoring et alerting

* Vérifier que le niveau de log est approprié.
* Logrotate sur les logs.

##Divers

* Vérifier que les tâches cron sont installées.
* Vérifier que l'envoi de mail se fait sans finir en spam.

##Référencement

* Enregistrer son site dans la Google Console.
* Fournir le sitemap à Google.
* Renseigner correctement le robots.txt
* Signaler la mise en ligne de son site aux autres moteurs de recherche : Qwant, Yahoo, Bing...

##Déploiement continu

* Vérifier que les bons fichiers sont conservés entre deux déploiements : contenus générés/uploadés, logs, etc.
