---
title: J'adore coder sans specifications
tags:
    - Savoir vivre de dev

---

Explication pour les profanes : normalement, quand on demande à une développeur de développer, on lui donne notre besoin précis. Des spécifications. Souvent, le développeur n'arrive pas à obtenir ces spécifications. Et généralement, ça l'énerve.

<!--more-->

Quand je n'arrive pas à obtenir de specs pour un développement que je dois réaliser, je suis heureux : ça veut dire que je peux faire ce que je veux !

#Need zo no, to win, again, ze no

Premier exemple concret : internationaliser un site web existant. J'ai vécu ce besoin trois fois. A chaque fois, les mêmes questions reviennent :

* Dans quels pays veut-on apparaitre pour commencer ? Et ensuite ?
* Comment gère-t-on les langues ? On en garde une seule ? Une langue par pays ? Plusieurs par pays ? On décorelle la langue du pays ?
* Mêmes questions pour les devises.
* Mêmes questions pour les taxes/TVA. En plus, certains pays en appliquent plusieurs, non ?
* Est-ce qu'on utilise un compte en banque spécifique à chaque pays ?
* Est-ce qu'on cloisonne les clients/utilisateurs par pays ?
* Un utilisateur peut-il changer de pays ? 
* Est-ce qu'un utilisateur du site français peut fournir une adresse de domicile dans un autre pays ?
* Que veut-on comme noms de domaines et routes ? Un nom de domaine par pays ? Une locale en préfixe de chaque route ? Est-ce qu'on traduit les routes ?
* Dans quelle devise envoie-t-on nos rapports de ventes à nos partenaires/fournisseurs ?
* Comment fait-on pour calculer des statistiques de ventes si on les réalise dans plusieurs devises différentes ?
* On doit convertir des prix dans d'autres devises ? En utilisant quel taux ? On convertit au moment de la commande ou bien plus tard ?
* ...

Il n'y a pas de réponse unique à ces questions. Tout dépend du produit, du contexte, de la société, et aussi un peu de ce qui arrange les développeurs.

Au final, le besoin business il se fout de pas mal de ces questions au début. Lui, il stipule juste "je veux vendre mes articles en Allemagne et en Suisse".

De mon expérience, c'est généralement le développeur qui demande des eclaircissements sur ces points. Le fonctionnel saura répondre rapidement au premier tiers de ces questions. Il répondra avec réflexion au deuxième tiers. Il répondra puis se contredira à maintes reprises sur le troisième tiers. Et enfin, il ne saura pas du tout répondre au dernier tiers.

Oui, ça fait quatre tiers. [Mais tout dépend de la taille des tiers, c'est Marcel Pagnol qui le dit](http://www.marcel-pagnol.com/biblio-marius,8.html).

Bref, le développeur est  livré à lui même concernant deux petits tiers (qu'on peut arrondire à la moitié, c'est bon vous suivez ?) des questions qui le taraudent. Généralement, c'est là que la dépression commence. Personnellement, ça m'excite pas mal. C'est le moment où je peux sortir de mon quotidien de pissage de code pour aller parler avec des vrais gens et leur soumettre des idées (qui généralement me font faire le moins de développement possible).

Pour moi la solution réside dans l'usage de ces trois trucs :

* l'agilité
* le déploiement continu
* le feature toggle

On ne sait pas trop où viser ? Et bien on va essayer un truc, le déployer rapidement , analyser, corriger le tir, et recommencer. On retrouve très vaguement le principe du [Lean](http://www.infoq.com/fr/presentations/lean-startup-autour-petite-mousse).

Généralement, on a beau discuter d'un besoin avec un fonctionnel, au bout de quelques dizaines de minutes de dialogue, tout est devenu trop abstrait pour qu'on se comprenne. Le développeur a le code en tête, il voit exactement ce qu'il peut faire. Mais le fonctionnel est dans le flou total (sans forcément s'en rendre compte). Le fait de **faire un truc**, aussi petit soit-il, permet de montrer quelque chose au fonctionnel de tangible, pour qu'il prenne ses repères et qu'il visualise mieux une problématique afin de définir la prochaine étape.

Ainsi, on procède par petites étapes, on essaie différentes choses, on tatonne. Parfois on fait fausse route, on doit reculer et retirer du code. Deuxième étape de la démoralisation du développeur : modifier/virer des trucs qu'il vient de faire. Personnellement, je m'en bats les steacks. Je suis payé pour faire tout ça, et il est convenu avec le fonctionnel que l'on avance ainsi. C'est le jeu.

Là ou ça devient un poil lourd, c'est quand il faut modifier la base de données. Du code, ça s'ajoute et se retire à volonté sans problème. La base de données par contre, elle se manipule avec précaution. Il faut utiliser un système de migrations robuste, et tenir compte de toutes ces difficultés :
* Modifier une grosse table, ça la vérouille et rend donc le site potentiellement indisponible pendant plusieurs secondes/minutes.
* Pour renommer un champ en toute sécurité, il vaut mieux parfois en créer une copie à côté et effacer l'ancien plusieurs heures après.
* Dès qu'on joue beaucoup avec les migrations, il devient difficile de travailler à plusieurs en parallèle sur le projet sans avoir de collisions.

#Pimp my site

Second exemple : le site corpo d'une société éditrice. C'est généralement très vieux et moche.
