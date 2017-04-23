
---
title: Un tableau de bord dans l'open space
tags:
    - Dev

---

![](/images/board1.jpg){.img-responsive}

Pourquoi, comment, où, quand.

<!--more-->

##Pourquoi faire ça ?

Je vais surtout vous parler tout au long de l’article de ce qui a été provoqué par la mise en place de ce genre de board dans les boites que j’ai vues. On peut avoir des arguments de vente pour ce genre d’outil, mais le meilleur reste ce que l’on observe à posteriori : plein de choses inattendues qui sont spécifiques à chaque milieu.

##Quand le mettre en production ?

Le plus tôt possible ! Créez une page html tout dégueulasse avec un compteur de je-ne-sais-quoi (visiteurs, ventes), et affichez la ! Cela va déjà prendre du temps de faire ça.

Si on n’a pas l’habitude, c’est le moment de faire du lean sans faire dans sa culotte : le projet est à usage interne, on ne craint rien. Il faut en profiter pour commencer petit.

L’image en haut d’article est un bon exemple de la méthode : c’est moche, c’est incomplet, on a une courbe des ventes qui déconne totalement, mais c’est là, ça suscite des réactions, c’est amélioré peu à peu.

###Initier le projet

Des coûts indivisibles de mise en place, quelle que soit la complexité du projet  :

* repository de code ;
* sécurisation : check par IP, Htaccess ou équivalent ;
* gestion des déploiements avec redémarrage et actualisation automatique.

###Afficher le board

Il faut d’abord trouver un écran. Sur la photo de l’article, vous avez une belle TV accrochée au mur. Dans un premier temps, un moniteur 17 pouces tout dégueulasse posé sur une étagère peut faire l’affaire.

Concernant le PC qui fait tourner le navigateur : on a toujours une vieille brouette qui traîne dans un coin. Il faut juste garder à l’esprit qu’elle va tourner 24/7. Le Raspberry Pi peut être une solution séduisante, mais il a une grosse contrainte : quand on n’a pas trop envie de bidouiller, difficile de trouver les dernières versions de navigateurs dessus. Donc, ne pas trop faire le fou-fou au niveau CSS3. Et puis c’est lent à mourir.

###Faire vivre le projet

Une fois l’écran affiché, il va naturellement attirer les gens et générer un important nombre de retours/idées géniales/suggestions. Cool ! C’est ce qui va guider l’évolution du board. Attention toutefois à ne pas se précipiter : beaucoup d’idées venant de différentes personnes vont être incompatibles entre elles. Attendre d’avoir plusieurs retours qui vont dans le même sens avant d’implémenter une fonctionnalité. Mais ne pas hésiter à essayer des choses non plus, quitte à rollbacker ensuite.

###On le met où ce bousin ?

N’import où tant qu’on peut s’arrêter devant, en discuter à plusieurs. A côté d’une machine à café. Attention à ne pas le faire trop clignoter ou à l’animer : cela peut déconcentrer les gens qui l’ont dans leur champ de vision à partir de leur poste.

##Concrètement, ça donne quoi ?

Deux cas vécus différemment dans deux boites.

###Librato Metrics + statsd, affiché publiquement

![](/images/board2.png){.img-responsive}

Cet outil, c’est du bonheur en barre. Ou plutôt en courbes. Ça prend en entrée des données, et ça en ressort des courbes. Get it ? L’outil met à disposition une API REST pour pousser des données, mais surtout un connecteur Statsd pour avoir des statistiques en temps réel. Il ne reste plus qu’à savoir ce qu’on veut surveiller.

Dans le cas que j’ai vécu, on voulait monitorer un jeu casual par navigateur : un quiz dont chaque partie dure quelques dizaines de secondes. Nous avons donc traqué l’action de lancer une partie, pour être sûr d’avoir du volume. Mais cela peut être des pages vues, des requêtes HTTP, des commandes de produits (si vous êtes forts et que vous en avez plein). L’idée est d’avoir la plus grosse volumétrie possible afin d’obtenir une courbe régulière et plate. Par dessus cette courbe, on affiche des jalons correspondant aux mises en production. Et on obtient une solution béton pour détecter les déploiements qui pètent tout : lorsque la courbe s’effondre, on sait que le stagiaire a tout cassé.

Une fois cet outil utilisé avec abus par les développeurs, on l’a affiché dans l’open space avec du matériel de récupération : un vieux pc sous windows, et un écran 14 pouces. Et là, ça a un peu été un peu compliqué : fuites mémoires de l’OS, du navigateur, du site. On pensait qu’on aurait juste à lancer l’appli et la faire tourner jusqu’à la nuit des temps. On s’est rendu compte qu’il fallait la maintenir. Incroyable.

Donc, ne pas perdre de vue le fait qu’il s’agit d’un projet à part entière, qui demande à être entretenu. Il n’y a rien de plus triste qu’un écran noir au mur, avec les fils qui pendouillent.

Le board a aussi été victime de son succès : en plus d’afficher la courbe de monitoring, il affichait des données d’utilisation directement compréhensibles par le fonctionnel. Le truc fabuleux, c’est que les gens du business sont devenus accros à ce board. Le truc moins marrant, c’est qu’avec statsd, on avait environ 10% de perte de données à cause de l’UDP. On aurait surement pu l’améliorer, mais ce n’était pas notre besoin au niveau technique : on se foutait des chiffres, on voulait juste voir les évolutions des courbes et les tendances. Mais ça, ça ne colle pas avec des gens du fonctionnel qui ont besoin de chiffres précis.

###Dashing

La solution utilisée comme image d’illustration de l’article. Orientation totalement différente de la précédente solution. Le contexte est, en gros, une boite de e-commerce. On affiche un ensemble de widgets fournissant des informations variées de manière très graphique :

les derniers articles vendus ;
une courbe des ventes ;
des compteurs de plein de trucs ;
les best-sellers ;
une zone de texte qui affiche le dernier message saisi sur le chat interne. Inutile donc indispensable ;
Le plus instructif est sans conteste le premier point : regardez régulièrement ce que vous vendez à divers moments de la journée, et vous en tirerez des informations « au jugé », très vagues, mais qui vont servir de base pour de futures recherches statistiques. Nous, on s’est rendu compte qu’on vendait un type de produit bien particulier à certaines heures bien définies de la journée, avec une précision assez effrayante.

Concernant les best-sellers, pensez à les calculer sur les x derniers jours ou semaines : un calcul sur la nuit des temps provoque des résultats qui ne changent jamais. Evidemment, on est excités comme des puces tous les 36 du mois lorsqu’un challenger vient faire bouger le score. Bref, c’est chiant comme un match de foot.

Les compteurs ne sont pas spécialement intéressants au premier abord. Mais mettez en plein quand même : quand un compte rond est atteint, ça motive le patron à payer l’apéro.

Concernant la technique : on a utilisé Dashing. C’est sympa, simple. Notez leur tagline humble. En ce moment je galère à le redémarrer proprement et sûrement par contre. Saloperie.

##Conclusion

Je termine avec un ressenti de développeur : ce genre de projet, ça fait du bien. Nous l’avons pris comme un side-project. On y travaille de temps en temps à la pause de midi ou le soir, selon notre bon vouloir. Si un vrai besoin venant du fonctionnel est énoncé, cela passe en story dans nos engagements. Mais l’aspect récréatif est important : il m’arrive de passer des stories entières à réaliser des tâches de maintenance de l’infra, qui ne se voient pas immédiatement du côté du client final. Avec ce projet comme exutoire, je peux réaliser quelque chose de simple, concret, visuel, en regardant les sourires de mes collègues découvrant la mise à jour.

C’est peu comme quand je m’enfile plusieurs films de Terrence Malick d’affilée, et que je termine par un bon gros Transformers pour décompresser.
