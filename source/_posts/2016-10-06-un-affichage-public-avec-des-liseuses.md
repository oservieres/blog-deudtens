---
title: Un affichage public avec des liseuses
tags:
    - Bidouillages

---

J'ai fait ce truc qui consiste à afficher les informations d'une salle de réunion sur un écran de liseuse :

![](/images/liseuse_2.jpg){.img-responsive}

<!--more-->

Le principe est simple : l'écran est affiché à l'entrée de la salle. Il indique quelle est la réunion en cours ainsi que jusqu'à quand elle a lieu. De la même manière, il indique la prochaine réunion et à quelle heure elle commence. Dans notre cas, les réservations des salles sont entrées dans Google Calendar. Ce sont ces informations qu'on affiche.

#À quoi ça sert ?

* À m'amuser ;
* à rendre un peu plus concrètes les réservations de salles qui se font sur ordinateur ;
* à satisfaire rapidement notre curiosité quand on passe devant la salle, qu'on y voit un attroupement de personnes, et qu'on se demande de quoi ça parle ;
* à régler les malentendus quand deux groupes se disputent une salle, chose qui arrive de plus en plus à mesure que l'entreprise croît ;
* conséquence du précédent point : à sensibiliser les collègues à la réservation de salle plutôt que de faire de l'occupation YOLO.

#Pourquoi afficher ça sur des liseuses ?

Les liseuses ont un écran E-ink, dont une des spécificités est que bien utilisé, il ne consomme quasiment pas d'énergie. En tout cas beaucoup moins qu'un écran LCD. [Mon estimée collègue Agnès explique bien le principe](https://tut-tuuut.github.io/2014/06/30/un-site-web-pour-liseuse.html).

Ce projet est aussi l'occasion de réutiliser les quelques vieilles liseuses de test obsolètes dont on dispose sur mon lieu de travail, qui ne sont plus tellement en état de marche.

#L'installation

##Considérations générales

Je le dis tout le temps, et j'aime bien le répéter : mettre en place un affichage public qui fonctionne et qui dure dans le temps, c'est très difficile. Il y a une infinité de contraintes physiques, matérielles et logicielles qu'on n'anticipe pas, surtout quand on ne travaille pas dans ce domaine. On a tendance à sous-estimer ces difficultés et arriver la gueule enfarinée le jour du déploiement pour se rendre compte qu'il y a un problème. Le genre de problèmes que j'ai vécus ou vus autour de moi :

* vous voulez afficher des infos sur une télévision, mais elle se met en veille au bout de 3 heures.
* vous voulez mettre en veille la télévision lors de la fermeture et la rallumer automatiquement. Elle sait le faire, sauf que son firmware est buggé, ça ne marche pas.
* vous voulez afficher le contenu d'une page d'un site tiers sur un écran, mais elle a des fuites de mémoire en javascript, ça fait tout planter au bout de 2 jours.
* vous voulez afficher une grosse image au hasard sur votre TV, mais le mini-pc qui est censé l'afficher est à la peine et plante dès qu'il se prend du 4000x3000.
* vous vous appelez Leclerc, vous construisez une énorme extension de votre magasin consacrée aux loisirs et à la culture, et vous y vendez des produits de riches. Vous installez un écran géant sur la façade extérieure. 1 semaine après l'ouverture, trois grosses zones de pixels morts apparaissent.

Une fois que ces problèmes non-anticipés apparaissent, on les laisse généralement trainer, et on se retrouve avec un truc visible par tous et qui ne marche pas. Le résultat est déprimant.

On a aussi tendance à oublier que ces affichages nécessitent de la maintenance. Celle-ci a un coût plus élevé que celle d'un site web, vu qu'elle nécessite des opérations physiques.

##Notre cas

Tadaaaa :

![](/images/liseuse_1.jpg){.img-responsive}

On a donc une liseuse patafixée au mur, avec le câble de charge qui part vers la prise. J'aurais aimé me passer de ce câble pour utiliser la batterie, quitte à brancher la liseuse tous les 10 jours pour qu'elle se recharge. Mais l'application bouffe la batterie en une journée : c'est une première version, je n'ai pas du tout réfléchi à comment optimiser la consommation électrique. Il y a clairement moyen de faire mieux, ce qui serait souhaitable vu que l'utilisation d'un chargeur annule un peu l'intérêt d'avoir un écran E-ink.

Au niveau de la mise en place, sur la première salle de la réunion, ça s'est plutôt bien passé. L'appli plante environ une fois par semaine pour je-ne-sais-quelle raison. Peut-être une fuite mémoire. Mais j'arrive avant les collègues, il ne savent pas que je la redémarre et pensent que j'ai livré un produit d'une robustesse incommensurable. Donc tout va bien, hein ?

J'ai essayé d'étendre mon territoire à deux autres salles de réunions, mais les liseuses ont été un peu plus récalcitrantes : il s'agissait de modèles particuliers, sur lesquels des expérimentations perverses avaient déjà eu lieu. Je crois que j'en ai achevé une alors qu'une autre se décharge continuellement. Tout simplement car j'ai utilisé des rallonges USB pour la charger, et il semblerait que la tension en prenne un coup.
On tombe en plein dans les problèmes relous dont je parlais plus haut. Et c'est galère à gérer.

##Au niveau logiciel

[Le code est open source](https://github.com/oservieres/getaroom). Mais attention, c'est **le code le plus dégueulasse du monde**. Vraiment. Ne me jugez pas. C'est un projet fait sur les pauses de midi pour rigoler. De plus, étant naturellement sous-doué en C, le code de l'appli est particulièrement ignoble.

Il y a deux composants :

* une application native pour liseuse Pocketbook codée en C++ ;
* un serveur interrogé par l'application native qui recupère les données chez Google.

J'aurais pu choisir de tout faire dans l'application native de la liseuse, mais j'en ai décidé autrement. La raison officielle, c'est qu'il est toujours bon d'externaliser de l'intelligence côté serveur tant que c'est possible, afin de pouvoir en bénéficer sur d'autres types de clients.
La raison officieuse, c'est que j'avais gravement la flemme de coder un client oAuth en C sur la liseuse pour accéder aux API de Google.

Le code du serveur tourne sur un petit serveur local qui se trouve dans nos locaux. Ce qui explique qu'il n'y a aucune couche de sécurité dessus.

#Et après

Il y a plein d'améliorations à envisager, j'ai déjà saisi quelques issues sur Github. Si vous aussi vous avez des vieilles liseuses Pocketbook à recycler, on peut s'entendre.
