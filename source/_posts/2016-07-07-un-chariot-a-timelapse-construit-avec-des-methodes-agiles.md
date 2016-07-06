---
title: Un chariot à timelapse construit avec des méthodes agiles
tags:
    - Savoir vivre de dev
    - Agile
    - Bidouillage

---

J'ai toujours l'impression de montrer un canif à une poule quand j'essaie d'expliquer les méthodes agiles, ou même comment je travaille, à des non-développeurs. Je raconte dans ce billet comment j'ai construit un chariot à travelling pour timelapse en utilisant une partie des raisonnements que je réserve d'habitude au développement web.

![](/images/timelapse/v6-1.jpg){.img-responsive}

<!--more-->

# Le besoin

Je veux faire un truc comme ça :

![](/images/timelapse/pro.jpg){.img-responsive}

Et ce truc permet de faire des trucs comme ça :

![](/images/timelapse/exemple.gif){.img-responsive}

Bon, ce plan en particulier n'a pas été fait avec exactement ce matériel (sinon on verrait le rail), mais vous voyez le principe : on prend une photo toutes les x secondes sur un chariot qui avance très lentement, et on balance ça à 25 images/seconde ensuite.

Plus précisément, voici mes besoins :

* je veux faire un travelling sur 1 mètre minimum, plus que ça si possible ;
* le machin doit rentrer dans une valise pour voyager avec ;
* le truc doit être construisible par moi, qui ne sait pas beaucoup bricoler ;
* la chose doit me coûter (beaucoup) moins de 100 €. En acheter un dans le commerce coûterait au moins 7 fois plus que ça ;

Teasing : on verra à la fin que je n'avais en fait pas vraiment ces besoins là. Comme en informatique, on pense souvent savoir ce que l'on veut, mais c'est rarement en adéquation avec ce dont on a vraiment besoin.

# Itération 1 : le prototype en LEGO

*Pour info, j'avais déjà fait un article sur ce prototype, sur l'ancienne version du blog. Je n'ai pas pris la peine de le réimporter, tout est dans ce paragraphe.*

Je ne sais pas encore si je veux vraiment faire ce projet : ça va me coûter du temps et de l'argent. Pour m'aider à me décider, je construis une première version en LEGO.

![](/images/timelapse/lego.jpg){.img-responsive}

Ca donne ça :

<iframe width="700" height="470" src="https://www.youtube.com/embed/mfd9v-C3qfw" frameborder="0" allowfullscreen></iframe>

C'est plutôt convaincant pour un machin bidouillé en une après midi chez papa et maman. Cependant, il y a des limitations :

* ça fait un bruit de fou ;
* il faut que le chariot avance sur un sol/support parfaitement lisse ;
* pas possible de faire progresser le chariot en pente/verticalement ;
* il faut que je rende les LEGO à mes neveux maintenant.

Je me suis bien amusé, mais je me suis lassé du projet : finalement, maintenant que j'ai le prototype entre les mains, je n'ai plus trop envie d'y passer du temps. Je me rends compte que je ne sais pas faire de time lapse. je vais d'abord passer du temps à maitriser la technique sans mouvement de caméra.

Et ne me traitez pas de gamin capricieux qui change de jouet après 5 minutes : au travail, mon quotidien, c'est de mettre en pause des tâches en cours pour lancer des tâches de toute urgence qui seront mises en pause pour lancer d'autres tâches de toute urgence.

# Itération 2 : le MVP

Quelques mois plus tard, j'ai fait [plusieurs time lapses fixes ou bien avec un peu de pivots](https://www.youtube.com/watch?v=fNC9h53wSHc), et je commence à m'ennuyer. L'envie de mouvement revient. On ressort le projet du grenier !

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

* l'appareil photo tient mal, posé bêtement ;
* le chariot est propulsé par la force du bras. Je préférerais qu'il avance tout seul ;
* le rail est trop grand pour rentrer dans une valise ;

Mais cette première version me permet de vérifier la faisabilité du bordel. De plus, je n'ai aucune idée de comment régler les 3 problèmes cités. Le fait d'avoir cette première version sous les yeux, de pouvoir la tripoter et la mesurer, me permet de réfléchir à la suite. Tout ça en vissant trois planches, deux bouts de feraille et quelques roulettes, c'est déjà bien.

Je fonctionne pareil avec mes projets web : je les simplifie à outrance, parfois même jusqu'à l'absurde en apparence, pour les déployer sur le net le plus vite possible et les faire évoluer ensuite.

# Itération 3 : la transportabilité

A ce moment là, j'aimerais travailler sur la motorisation, afin d'avoir un objet pleinement fonctionnel et faire des essais avec. Malheureusement, je n'ai pas encore reçu les pièces détachées pour celà. Ainsi, je me rabats sur des tâches moins urgentes. Je verrai plus tard que c'était une erreur, et que j'aurais du mettre le projet en pause.

Le choix que je fais, c'est de couper mes rails en deux afin de les faire rentrer dans la valise. Mais avant cela, je fixe d'abord les pattes qui assembleront les morceaux de rails :

![](/images/timelapse/v2-1.jpg){.img-responsive}

Tant que j'y suis, je prépare des renforts pour quand mon système sera coupé en deux :

![](/images/timelapse/v2-2.jpg){.img-responsive}

C'est le moment de dégainer la scie :

![](/images/timelapse/v2-3.jpg){.img-responsive}

Une fois le bordel remonté, on obtient un magnifique rail en kit :

![](/images/timelapse/v2-4.jpg){.img-responsive}

Au niveau budget, il y a pas mal de pattes, de vis et d'écrous papillons. Il doit y en avoir pour une dizaine d'euros.

J'insiste sur le fait d'avoir rajouté les morceaux de feraille avant d'avoir coupé les rails : cela permet de minimiser le temps pendant lequel mes rails sont inutilisables. De plus, cela apporte une sécurité de travailler sur un rail encore fonctionnel avant d'entamer la partie critique. Je ne lâche pas ma branche avant d'avoir saisi la prochaine. En informatique, ça peut s'apparenter à du feature toggle : on peut prendre du temps pour développer une fonctionnalité, ce n'est pas grave, tant que l'ancien système continue à fonctionner.

**Le bonus** : je peux maintenant intercaler autant de rails que je veux entre mes deux parties principales !

![](/images/timelapse/v2-5.jpg){.img-responsive}

Par contre, il y a un **bug** : quand le chariot passe sur la jonction entre deux rails, il subit une légère secousse. J'espère que ce n'est pas grave, et que le tremblement ne se ressentira pas sur une avancée très lente du chariot. Mais je n'ai pas encore ce problème. Je verrai en temps voulu lors de mes premiers tests. En attendant, je peux vivre avec ce bug.

C'est l'occasion de me rappeler pourquoi je préfère d'habitude réfléchir en [KISS](https://www.techopedia.com/definition/20262/keep-it-simple-stupid-principle-kiss-principle) : les systèmes les plus simples sont ceux qui marchent le mieux. En complexifiant mon rail, j'ai rendu son fonctionnement plus ardu et ai engendré de nouveaux problèmes.

# Itération 4 : la fixation de l'appareil photo

J'ai acheté une tête de trépied à 18 € et je l'ai vissée au milieu de mon chariot.

![](/images/timelapse/v4-1.jpg){.img-responsive}

Je crois que c'est le composant le plus cher de mon projet. J'aurais pu bricoler un truc moi même, mais ça n'aurait pas été aussi bien fait et ça m'aurait pris beaucoup de temps. En informatique, on peut faire le parallèle avec les dépendances d'un projet : plutôt que de faire un truc soit-même, on investit dans l'utilisation d'une brique existante, quitte à ce qu'elle fasse un peu trop de choses et qu'elle soit un poil lourde. Notez que même quand cette dépendance est libre/opensource/trucquialairgratuit, elle a un coût : de maintenance, de mise à jour et d'évolution.

Au passage, j'ai récupéré divers morceaux d'attaches pour Gopro ainsi qu'une perche et j'ai fait une mini grue :

![](/images/timelapse/v4-2.jpg){.img-responsive}

L'intérêt, c'est de pouvoir faire des plans au ras du sol sans que l'on voie le rail. J'ai aussi une idée malsaine de travelling vertical qui finirait dans l'eau. J'ai hâte de pouvoir tester.

![](/images/timelapse/v4-3.jpg){.img-responsive}

# Itération 5 : réflexion sur la motorisation

J'ai plusieurs solutions en tête. La question, c'est "comment entraine-t-on le mouvement ?" :

* [avec une couroie](http://www.instructables.com/id/DIY-motorized-moving-timelapse-camera-dolly-with-A/) ;
* [avec une crémaillière](https://www.youtube.com/watch?v=hVYeO-F-8kA) ;
* [avec un fil](http://www.instructables.com/id/DIY-Time-lapse-Dolly/) ;
* [avec une tige filetée](https://youtu.be/AL9svapX_T4?t=4m1s).

La couroie, j'oublie tout de suite : ça a l'air d'être une pièce très compliquée à trouver, encore plus à la bonne taille. Sans parler des roues crantées. la crémaillière me fait moins peur, mais je suis pas trop chaud non plus. Ça implique de mettre le moteur sur la partie mobile, ça me semble trop compliqué.

Tirer le chariot avec un fil, c'est très con, très moche, mais ça marche. En plus, ça me permet de ne pas réfléchir à la longueur de mes rails : le système est extensible. Faire attention quand même au fil à utiliser : s'il se détend, on risque d'obtenir un mouvement irrégulier.

La tige filetée, je trouve que c'est une solution très classe. C'est propre, c'est joli à voir. Mais comment faire avancer le chariot rapidement en cas de besoin ? De plus, la longueur de la tige est problématique : il faut qu'elle rentre dans ma valise. Et cela m'empêche de rendre mes rails plus longs, vu que la longueur de la tige doit suivre. Dommage car je trouve que d'un point de vue conceptuel, l'idée est très belle.

Bref, je pars sur l'idée du fil pour l'instant. L'avantage, c'est qu'elle ne coûte rien qui lui soit spécifique, en dehors du fil. Je pourrai réutiliser les autres matériaux si jamais je pars sur une autre solution au final.

On est aussi souvent confronté à ce genre de cas quand on programme : pour un besoin donné, une multitude de solutions s'offrent à nous. Il faut préparer le développement en amont, réfléchir, challenger les choix, changer d'avis et trancher. C'est une des raisons pour lesquelles les estimations sont difficiles à réaliser.

En utilisant la solution de la tige filtée, j'aurais fait de l'[overengineering](http://www.codesimplicity.com/post/what-is-overengineering/). J'aurais pu me gargariser d'avoir quelque chose d'intellectuellement flatteur, mais j'aurais été bien emmerdé par la complexité du truc et l'évolutivité réduite..

# Itération 6 : réalisation de la motorisation

Première étape, je mets en place le minimum nécessaire à l'action du chariot, un fil :

![](/images/timelapse/v3-1.jpg){.img-responsive}

Notez que la boucle et le petit mousqueton sont **chers sa race**. Je n'ai plus les prix en tête, mais en tout il y en a pour facilement 10 €. Préférez de la récupération.

Je peux maintenant précisément tirer mon chariot... à la main. J'ai l'air con, ça va me prendre du temps et de l'énergie lorsque je ferai un timelapse, et puis ça ne sera pas très précis, mais c'est faisable. Chers chefs de projets, quand vous me demandez de faire un truc à moitié fini quitte à faire des choses à la main ensuite, ça donne ça.

Vient le temps de la motorisation. Pour celà, j'ai commandé :

* un moteur 12V DC avec réducteur qui tourne à 2 tours/minute ;
* un variateur de vitesse ;
* une prise d'alimentation jack femelle ;
* un boitier pour enfermer tout ça ;
* un mandrin de perceuse pour enrouler le cable.

Il y en a pour environ 25 € en tout.

J'ai assemblé le tout sommairement avant de vraiment percer des trous dans mon boitier. Ça donne ça :

![](/images/timelapse/v5-1.jpg){.img-responsive}

Le tout est alimenté par un transformateur de 12V trouvé sur un routeur qui pourrissait au fond d'un tiroir. À terme, j'achèterai une batterie.

# Premier test

Le dispositif :

![](/images/timelapse/v5-2.jpg){.img-responsive}

Le résultat :

<iframe width="700" height="470" src="https://www.youtube.com/embed/OQZ8hvfesWA" frameborder="0" allowfullscreen></iframe>

C'est la catastrophe. C'est de la merde. La caméra part dans tous les sens. Ce n'est pas stable. Essayons de mettre un coup de stabilisateur avec After Effects :

<iframe width="700" height="470" src="https://www.youtube.com/embed/YpX1UmJUAe0" frameborder="0" allowfullscreen></iframe>

C'est tout autant dégueulasse. J'ai foiré. Il faut tout revoir.

# Rétrospective

Analysons les causes de l'échec. Mon rail fonctionne mal. Lorsque le chariot passe sur des jonctions, il bouge, et cela rend l'image instable.

Mais pire que ça, je me rends compte que j'ai construit un objet qui ne me sert à rien :

* OK, le rail fait 1m50, c'est super. Mais je me rends compte que je n'ai pas besoin d'autant de longueur. Le tiers de cela me suffit pour faire un petit travelling sympa.
* Le machin que j'ai construit est LOURD. Comme quand on développe une usine à gaz en informatique. On dit souvent que c'est lourd. Ben là c'est pareil, sauf que c'est littéralement lourd.
* le mouvement est rapide. Moi, ce que je veux, c'est un travelling très lent, voir imperceptible, pour donner juste un peu de profondeur et de parallaxe à l'image. Quelque chose de doux, subtil et maitrisé, comme moi. Un mouvement lent implique qu'on a encore moins besoin d'une grande longueur de rails.

Bref, je me suis focalisé sur l'extensibilité alors que je n'en avais pas besoin. Je ne vais même pas chercher à régler ce problème de secousses sur les jonctions : je n'ai plus besoin des jonctions.

En disant ça, je fais quelque chose que j'ai trop peu vu dans ma vie de développeur : j'abandonne une fonctionnalité. J'aimerais que ça arrive plus souvent, mais il y a toujours une (mauvaise) raison de garder cet écran de backend pourri qui plante constamment, ou bien cette fonctionnalité de recherche avancée que personne n'utilise.

# Itération 7 : correctif

Je retourne à Leroy Merlin acheter des profilés en fer beaucoup plus légers. Et je les coupe à la bonne longueur pile pour qu'ils rentrent dans ma plus grosse valise : 75cm. Aussi, je rajoute une equerre entre mon rail et mon boitier moteur, afin de pouvoir séparer les deux facilement pour le voyage. Et hop :

![](/images/timelapse/v6-1.jpg){.img-responsive}

Le résultat en action :

<iframe width="700" height="470" src="https://www.youtube.com/embed/C3iXwcACyYY" frameborder="0" allowfullscreen></iframe>

C'est beaucoup mieux ! Je pense aussi que le fait d'aller plus lentement aide un peu.

# Itération 8 : Fine tuning

Nouveau problème : mes nouveaux rails sont flexibles à cause de leur légereté. Ils plient sous le poids du chariot et de l'appareil. j'imagine que c'est la cause du léger "flottement" qu'on voit à l'écran. Je décide de récupérer des élements de l'ancien rail pour consolider le tout :

![](/images/timelapse/v7-1.jpg){.img-responsive}

Le résultat (après stabilisation de micro-secousses sous After Effects) :

<iframe width="700" height="470" src="https://www.youtube.com/embed/o3PMP3Nn5oE" frameborder="0" allowfullscreen></iframe>

Ca commence a être vraiment bien. Au passage, j'ai fait plein de petites améliorations :

* J'ai tout installé à sa place finale dans mon boitier.
* Le fil avait tendance à mal s'enrouler autour du mandrin. Une pièce en plastique ronde permet maintenant de guider le fil.
* La télécommande trainait et déstabilisait surement l'appareil quand elle était enroulée autour. Je l'ai fixée au boitier moteur avec du velcro.
* J'ai rajouté un inverseur bipolaire (l'interrupteur, là) pour changer le sens de rotation du moteur.

# Et après

Idée : il faudrait que le chariot s'arrête lorsqu'il arrive en butée. Il faudrait que je rajoute un interrupteur actionné par le chariot lorsqu'il vient au contact. En attendant, je dois rester à côté de mon bordel pour le surveiller.

# Et encore après

Il y a un problème avec mon dispositif : le moteur tourne en continu, la caméra est en perpétuel mouvement. C'est une limitation qui provoque des symptômes lorsque l'on fait des expositions longues : le mouvement provoque du flou de mouvement non désiré. Dans la plupart des cas c'est imperceptible. Mais en cas d'exposition très longue, ça peut devenir moche.

D'un côté ça m'embête bien. Mais d'un autre côté, ça coûterait très cher de corriger ce point. Si un développeur et un chef de projet parlaient de ce problème, ça donnerait ça :

```
- (Chef de projet) Tu me fais un timelapse de nuit avec exposition longue steuplé ?

- (Développeur) Je peux, mais ça va être un peu flou.

- Pourquoi ? C'est pas flou d'habitude.

- Le fait que le chariot bouge en continu alors qu'on fait une exposition longue, ça rend les photos floues.

- Pourquoi vous n'avez pas prévu ça dès le début ?

- Vous nous l'avez pas demandé.

- Bon, faut réparer ça, mets-toi sur ce sujet, priorité numéro 1 :

- Ça demande 2 semaines de développement.

- Ok, en fait c'est pas urgent du tout, on le fait pas.
```

Je ne compte plus le nombre de fois dans ma vie de développeur où une tâche critique est devenue inutile dès que j'ai annoncé combien de temps elle allait prendre.

De temps en temps, vient ensuite le moment où le chef de projet essaie de négocier le développement de la fonctionnalité en faisant un peu de zèle auprès du développeur, qui, lui, n'est pas non plus tout le temps très coopératif et de bonne volonté :


```
- (Chef de projet) J'ai une idée : tu bouges le chariot d'un centimètre, tu l'arrêtes, tu prends une photo, tu bouges le chariot d'un centimètre, ainsi de suite.

- (Développeur) C'est pas facile.

- Bah t'as déjà un bouton ON/OFF sur ton rail, tu peux le faire non ?

- Oui mais ça veut dire que je dois rester à côté du rail pendant une heure pour l'actionner à la main. C'est stupide, il faut automatiser ce processus.

- Et c'est ça qui prend autant de temps ? Mais pourquoi ? J'ai l'impression que c'est juste deux branchements à revoir.

- Non, il faut quelque chose qui programme l'action du moteur à intervalles réguliers. Et puis il faut changer le moteur : il faut qu'il soit plus rapide pour rattraper la distance non parcourue quand la photo est en train d'être prise. Et il faut qu'il soit précis, donc il faudrait probablement passer à un moteur pas-à-pas pour plus de précision.

- Vas-y, je te donne le temps pour faire tout ça, par contre, garde le même moteur STP.

- Ah, j'oubliais : il faut aussi synchroniser la prise de vue de l'appareil avec l'avancée du moteur, pour qu'il ne prenne de photo que lorsqu'il est immobile. Je n'ai jamais fait ça, je ne sais pas faire. Je peux y arriver, mais je ne sais pas en combien de temps.

- On dit 3 jours ?

- Je ne sais pas.

- 3 et demi ?
```

Cette conversation, plusieurs fois vécue, comporte plein de grands classiques :

* l'argument du "ça se fait en 3 lignes de code" ;
* les contraintes au niveau des moyens donnés qui vont jusqu'à l'absurde : de la contrainte peut naître l'innovation, mais quand on est dans un sujet si technique, qu'on parle en fait du coeur du projet à un niveau très profond, il n'y a pas de secret, il faut y passer le temps nécessaire pour obtenir une solution de qualité ;
* le développeur à qui on doit tirer les vers du nez pour comprendre pourquoi le problème est compliqué. On se demande parfois si il ne se fout pas de nous.

# Un dernier test

Je me suis amusé avec ma Gopro en combinant mon chariot avec [une tête qui permet de faire des rotations de caméra](http://fr.aliexpress.com/store/product/MYRMICA-360-Degree-Time-Lapse-Pan-and-Tilt-Head-for-GOPRO-SLR-Iphone-Android-Phone-More/1048722_1667775543.html) (n'achetez pas ces merdes, faites les vous même, ce sont des minuteurs de cuisine mécaniques avec une vis sur le dessus, c'est fragile et ça ne supporte pas le poids).

Ça donne ça :

<iframe width=700" height="470" src="https://www.youtube.com/embed/-eXtHJn2i_Q" frameborder="0" allowfullscreen></iframe>
