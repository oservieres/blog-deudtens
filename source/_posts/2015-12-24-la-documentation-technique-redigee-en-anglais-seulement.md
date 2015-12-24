---
title: La documentation technique : redigée en anglais seulement
categories:
    - Dev
tags:
    - Documentation
    - Anglais

---
La documentation en français me fait souffrir.

*NB : cet article a été écrit juste avant un crash du site. Et puis avant le backup aussi tant qu'à faire. Je l'ai réécrit de tête.*

Dans chaque boite que j'ai faite, j'ai tout le temps rencontré la situation embarassante où l'on devait envoyer une documentation interne rédigée en français à un prestataire/client/partenaire ne parlant pas la langue.

Pour moi la solution est "simple" : on doit rédiger toutes les documentations en anglais. Evidemment, ça implique des contraintes : cela prend plus de temps et les erreurs/approximations/emplois de faux-amis (j'ai fait ce dernier hier) seront plus nombreux (encore que quand je vois certaines documentations torchées en français...).

Il me semble acceptable d'exiger d'un développeur qu'il soit capable de rédiger en anglais, même de manière sommaire : de toute façon, tout est déjà en anglais sur Internet, on est bien obligé de connaitre.

Le but est au final d'éviter de se reveiller la gueule enfarinée en se disant "shit, on doit livrer rapidement cette doc à tartampion, mais il ne va rien comprendre" et de faire ce genre de cagade dans l'urgence :

* les devs n'ont pas le temps de traduire la documentation technique (comprendre "on préfère qu'ils continue à pondre des features") ? Filons ça au chef de projet fonctionnel ;
* faisons une traduction partielle des sections qui sont susceptibles d'intéresser les destinataires, on complètera au besoin ;
* envoyons la doc en français avec quelques explications à l'arache par mail.

Maintenir une documentation en plusieurs langues ? [Je n'y crois pas du tout](http://symfony.com/blog/discontinuing-the-symfony-community-translations). A moins d'être outillé correctement (et donc d'avoir un besoin justifié là dessus), les deux versions seront désynchronisées au lendemain de leur création.

Mon argumentaire est mis à mal par [<3 un fantastique collègue <3](https://blog.pascal-martin.fr/) qui me renvoie à un titre de documentation traduite à la va-vite quand on en a eu besoin.Le titre de l'article contient 4 fautes, dont :

* une erreur de syntaxe le rendant incompréhensible
* le mot "connexion" écrit en français

Difficile de défendre le "tout en anglais" quand on voit ce genre de carnage. Mais j'imagine que ça veut "juste" dire qu'il est trop tard : il fallait mettre en place une culture de la documentation en anglais dès le départ. Avec les mesures et pratiques qui vont bien, comme par exemple, de la revue de documentation au même titre que la revue de code, comme le proposait [une autre estimée collègue](http://blog.as-i-am.fr/) en commentaire avant que je ne l'efface avec mon Wordpress.

Autre contre argument : on peut tomber sur des clients qui n'aiment pas l'anglais. On m'a déjà parlé de développeurs incapables de lire nos documentations en anglais. Ca me rend fou que ça existe, et qu'on doive se plier à ce genre de demandes des clients. Je n'arrive pas à imaginer que ces développeurs soient compétents. En nivellant par le bas ainsi, on baisse la qualité de ce qu'on produit.
