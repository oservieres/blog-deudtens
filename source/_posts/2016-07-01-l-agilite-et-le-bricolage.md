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

J'obtiens ainsi mon [MVP](https://fr.wikipedia.org/wiki/Produit_minimum_viable) :

* je peux bouger le chariot à la main
* je peux poser mon appareil photo sur le chariot

Au niveau budget :

* deux profilés en métal de 1m de long : 8€ pièce chez Leroy Merlin ;
* 4 roulettes : 1 € pièce chez Leroy Merlin ;
* du bois et des vis de récupération : 0 € ;

Bon, pour l'instant, il est un peu pourri ce chariot à travelling :

* l'appareil photo tient mal ;
* le chariot est propulsé par la force du bras. Je préférerais qu'il avance tout seul ;
* le rail est trop grand pour rentrer dans une valise ;

Mais cette première version me permet de vérifier la faisabilité du bordel. De plus, je n'ai aucune idée de comment régler les 3 problèmes cités. Le fait d'avoir cette première version sous les yeux, de pouvoir la tripoter et la mesurer, me permet de réfléchir à la suite. Je suis juste certain d'une chose : pour rendre le dispositif transportable, **je devrai pouvoir le démonter en deux parties pour le transport**. Pour l'instant, je vois comment faire : il suffit de couper les rails au milieu et de les relier avec des pates.

# Itération 3 : la motorisation

Je choisis cette problématique comme sujet prioritaire, car c'est celle qui me fait le plus peur. Je commence toujours par les choses les plus complexes, pour éliminer l'inconnu le plus vite possible. On garde les choses simples pour la fin.

J'ai plusieurs solutions de motorisation en tête. La question, c'est comment entraine-t-on le mouvement :

* [avec une couroie](http://www.instructables.com/id/DIY-motorized-moving-timelapse-camera-dolly-with-A/) ;
* [avec une crémaillière](https://www.youtube.com/watch?v=hVYeO-F-8kA) ;
* [avec un fil](http://www.instructables.com/id/DIY-Time-lapse-Dolly/) ;
* [avec une tige filetée](https://youtu.be/AL9svapX_T4?t=4m1s) ;

La couroie, j'oublie tout de suite : ça a l'air d'être une pièce très compliquée à trouver, encore plus à la bonne taille. Sans parler des roues crantées. la crémaillière me fait moins peur, mais je suis pas trop chaud non plus. Ca implique de mettre le moteur sur la partie mobile, ça me semble trop compliqué.

Tirer le chariot avec un fil, c'est très con, très moche, mais ça marche. En plus, ça me permet de ne pas réfléchir à la longueur de mes rails : le système est exensible. Faire attention quand même au fil à utiliser : s'il se détend, on risque d'obtenir un mouvement irrégulier.

La tige filetée, je trouve que c'est une solution très classe. C'est propre, c'est joli à voir. Mais comment on fait pour faire avancer le chariot rapidement en cas de besoin ? De plus, la longueur de la tige est problématique : il faut qu'elle rentre dans ma valise. Et cela m'empêche de rendre mes rails plus longs ultérieurement, vu que la longueur de la tige doit suivre. Je n'arrive pas à me sortir l'idée de la tête. Dans le doute, j'achète une tige chez Leroy merlin à 0.60 €. Dans le pire des cas, elle me servira à caler un meuble.

Bref, je pars sur l'idée du fil pour l'instant. L'avantage, c'est qu'elle ne coute rien qui lui soit spécifique, en dehors du fil. Je pourrai réutiliser les autres matériaux si jamais je pars sur une autre solution au final.
