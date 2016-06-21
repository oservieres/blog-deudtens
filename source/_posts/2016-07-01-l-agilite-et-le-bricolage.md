---
title: L'agilité et le bricolage
tags:
    - Savoir vivre de dev
    - Agile

---
J'ai toujours l'impression de montrer un canif à une poule quand j'essaie d'expliquer les méthodes agiles à des non-développeurs. Et l'agile, j'adore ça, je remplis ma vie perso d'agile. Je raconte dans ce billet comment j'ai construit un chariot à travelling pour timelapse en agile. Au passage, je fais des parallèles avec le monde informatique à grand coup de métaphores et de trolls.

<!--more-->

# Le besoin

Je veux faire un truc comme ça :

![](/images/timelapse/pro.jpg){.img-responsive}

Et ce truc permet de faire des trucs comme ça :

![](/images/timelapse/exemple.gif){.img-responsive}

Plus précisément, voici mes critères :

* je veux faire un travelling sur 1 mètre minimum, plus que ça si possible ;
* le machin doit rentrer dans une valise pour voyager avec ;
* le truc doit être construisible par moi, qui ne sait pas beaucoup bricoler ;
* la chose doit me couter (beaucoup) moins de 100 € ;

# Itération 1 : le prototype en LEGO

Je ne sais pas encore si je veux vraiment faire ce truc : ça va me coûter du temps et de l'argent. Pour m'aider à me décider, je construis une première version en LEGO.

![](/images/timelapse/lego.jpg){.img-responsive}

Ca donne ça :

<iframe width="420" height="315" src="https://www.youtube.com/embed/mfd9v-C3qfw" frameborder="0" allowfullscreen></iframe>

C'est plutôt convaincant pour un machin bidouillé en une après midi chez papa et maman. Cependant, il y a des limitations :

* ça fait un bruit de fou ;
* il faut que le chariot avance sur un sol/support parfaitement lisse ;
* pas possible de faire progresser le chariot en pente ;
* il faut que je rende les LEGO à mes neveux maintenant.

Je me suis bien amusé, mais je me suis lassé du projet : finalement, maintenant que j'ai le prototype entre les mains, je n'ai plus trop envie d'y passer du temps. Je me rends comtpe que je ne sais pas faire de time lapse. je vais d'abord passer du temps à maitriser la technique sans mouvement de caméra.

# Itération 2 : le MVP

Quelques mois plus tard, j'ai fait plusieurs time lapses fixes, et je commence à m'ennuyer. l'envie de mouvement revient. On ressort le projet du grenier !

Je commence à constuire une version "pour de vrai" :

![](/images/timelapse/v1-1.jpg){.img-responsive}

![](/images/timelapse/v1-2.jpg){.img-responsive}

J'obtiens ainsi mon [MVP](https://fr.wikipedia.org/wiki/Produit_minimum_viable) :

* je peux bouger le chariot à la main
* je peux poser mon appareil photo sur le chariot

Au niveau budget :

* deux profilés en métal de 1m de long : 2.5€ pièce chez Leroy Merlin ;
* 4 roulettes : 1 € pièce chez Leroy Merlin ;
* du bois et des vis de récupération : 0 € ;

Bon, pour l'instant, il est un peu pourri ce chariot à travelling :

* l'appareil photo tient mal ;
* le chariot est propulsé par la force du bras. Je préférerais qu'il avance tout seul ;
* le rail est trop grand pour rentrer dans une valise ;

Mais cette première version me permet de vérifier la faisabilité du bordel. De plus, je n'ai aucune idée de comment régler les 3 problèmes cités. Le fait d'avoir cette première version sous les yeux, de pouvoir la tripoter et la mesurer, me permet de réfléchir à la suite.

# Itération 3 : la transportabilité

Je choisis de traiter ce sujet en priorité car il est structurant : des choix que je vais faire ici vont découler mes contraintes pour la suite.

Le choix que je fais, c'est de couper mes rails en deux afin de les faire rentrer dans la valise. Mais avant cela, je fixe d'abord les pates qui assembleront les morceaux de rails :

![](/images/timelapse/v2-1.jpg){.img-responsive}

Tant que j'y suis, je prépare des renforts pour quand mon système sera coupé en deux :

![](/images/timelapse/v2-2.jpg){.img-responsive}

C'est le moment de dégainer la scie :

![](/images/timelapse/v2-3.jpg){.img-responsive}

Une fois le bordel remonté, on obtient un magnifique rail en kit :

![](/images/timelapse/v2-4.jpg){.img-responsive}

J'insiste sur le fait d'avoir rajouté les morceaux de feraille avant d'avoir coupé les rails : cela permet de minimiser le temps pendant lequel mes rails sont inutilisables. De plus, cela apporte une sécurité de travailler sur un rail encore fonctionnel avant d'entamer la partie critique. En informatique, ça peut s'apparenter à du feature toggle : on peut prendre du temps pour développer une fonctionnalité, ce n'est pas grave, tant que l'ancien système continue à fonctionner.

**Le bonus** : je peux maintenant intercaler autant de rails que je veux entre mes deux parties principales !

![](/images/timelapse/v2-5.jpg){.img-responsive}

Par contre, il y a un **bug** : quand le chariot passe sur la jonction entre deux rails, il subit une légère secousse. J'espère que ce n'est pas grave, et que le tremblement ne se ressentira pas sur une avancée très lente du chariot. Mais je n'ai pas encore ce problème. Je verrai en temps voulu. En attendant, je peux vivre avec ce bug.

# Itération 4 : la motorisation

J'ai plusieurs solutions en tête. La question, c'est comment entraine-t-on le mouvement :

* [avec une couroie](http://www.instructables.com/id/DIY-motorized-moving-timelapse-camera-dolly-with-A/) ;
* [avec une crémaillière](https://www.youtube.com/watch?v=hVYeO-F-8kA) ;
* [avec un fil](http://www.instructables.com/id/DIY-Time-lapse-Dolly/) ;
* [avec une tige filetée](https://youtu.be/AL9svapX_T4?t=4m1s) ;

La couroie, j'oublie tout de suite : ça a l'air d'être une pièce très compliquée à trouver, encore plus à la bonne taille. Sans parler des roues crantées. la crémaillière me fait moins peur, mais je suis pas trop chaud non plus. Ca implique de mettre le moteur sur la partie mobile, ça me semble trop compliqué.

Tirer le chariot avec un fil, c'est très con, très moche, mais ça marche. En plus, ça me permet de ne pas réfléchir à la longueur de mes rails : le système est extensible. Faire attention quand même au fil à utiliser : s'il se détend, on risque d'obtenir un mouvement irrégulier.

La tige filetée, je trouve que c'est une solution très classe. C'est propre, c'est joli à voir. Mais comment on fait pour faire avancer le chariot rapidement en cas de besoin ? De plus, la longueur de la tige est problématique : il faut qu'elle rentre dans ma valise. Et cela m'empêche de rendre mes rails plus longs, vu que la longueur de la tige doit suivre. Dommage car je trouve que d'un point de vue conceptuel, l'idée est très belle.

Bref, je pars sur l'idée du fil pour l'instant. L'avantage, c'est qu'elle ne coûte rien qui lui soit spécifique, en dehors du fil. Je pourrai réutiliser les autres matériaux si jamais je pars sur une autre solution au final.

Première étape, je mets en place le minimum nécessaire à l'action du chariot, un fil :

![](/images/timelapse/v3-1.jpg){.img-responsive}

Je peux maintenant précisément tirer mon chariot... à la main. J'ai l'air con, ça va me prendre du temps et de l'énergie lorsque je ferai un timelapse, et puis ça ne sera pas très précis, mais c'est faisable. Chers chefs de projets, quand vous me demandez de faire un truc à moitié fini quitte à faire des choses à la main ensuite, ça donne ça.

# Itération 5 : la fixation de l'appareil

# Pour plus tard

Il y a un problème avec mon dispositif : le moteur tourne en continu, la caméra est en perpétuel mouvement. C'est une limitation qui provoque des symptômes lorsque l'on fait des expositions longues :

Bref, le mouvement combiné à l'exposition longue provoque du flou de mouvement. Si un développeur et un chef de projet, tous deux de mauvaise foi, discutaient du problème, ça donnerait ça :

- *Développeur* : 
- *chef de projet* : 
