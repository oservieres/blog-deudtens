---
title: Mariage : un photobooth, c'est comme un site web
tags:
    - Agile
    - Bidouillages
    - Mariage

---

Le besoin : avoir dans un coin de la salle de mariage un espace photo, avec un appareil posé sur un pied qui prend des photos des gens. Comme [la dernière fois](/un-chariot-a-timelapse-construit-avec-des-methodes-agiles/), je raconte ça à grand coup de métaphores sur le développement web.

![](/images/buzzer/resultat1.jpg){.img-responsive}

<!--more-->

Cette fois-ci, pas de progression par itérations : je ne me marie qu'une fois, je n'ai droit qu'à un seul essai.

##La solution

Mettre à disposition des convives un énorme bouton rouge qui déclenche une photo lorsqu'on appuie dessus. Un gros bouton comme ça, ça serait cool :

![](/images/buzzer/modele.jpg){.img-responsive}

Joie, j'ai trouvé exactement ce modèle sur le net, [ici](http://www.robotshop.com/eu/fr/bouton-poussoir-enorme-100mm-rouge.html) à environ 9 € (+ autant de frais de port, urgh). Je l'ai collé en haut d'un socle fait avec des matériaux de récupération (chutes de contreplaqué et barres de fer). Il trône ici au milieu de tout le bordel de décoration du mariage :

![](/images/buzzer/preparation.jpg){.img-responsive}

Notez l'impeccable finition à base d'agrafage de chutes de papier peint.

Détail important : le socle est très haut. Pour éviter que les enfants ne s'excitent sur le bouton. A ce moment là, je me crois encore malin en pensant que ça va les arrêter.

##Fabrication

Ma première idée, c'était de trifouiller une télécommande infra-rouge, pour remplacer son bouton par mon gros bouton rouge. Mauvaise idée. Version courte : ça marche pas. Sombre histoire de soudures qui ne tiennent pas sur le circuit imprimé de la télécommande.

L'idée retenue au final, ça a été d'utiliser le bouton comme grosse télécommande filaire. Le [KISS](http://www.bouzin-agile.fr/?post/2013/03/12/KISS-Keep-it-Simple-Stupid) en application : ne pas s'embêter avec du sans-fil, des circuits imprimés et de l'infrarouge, la liaison par fil suffit, elle est plus simple, et elle fonctionne.

L'appareil étant un Nikon, j'ai du acheter un cable de télécommande qui a un embout propriétaire. J'ai carrément acheté la télécommande pour ne me servir que du fil, [ici](https://www.amazon.fr/D%C3%A9clencheur-distance-t%C3%A9l%C3%A9commande-filaire-MC-DC2/dp/B004AN7IAI). Ca coûte dans les 15 €. J'ai rajouté une rallonge de 5 mètres pour être tranquille.

Il me restait donc à raccorder l'autre côté du cable à l'interrupteur, ce qui se fait facilement une fois qu'on a trouvé quels fils raccorder à quelles bornes en essayant les combinaisons une par une. Attention : il y a une combinaison qui marche presque, mais qui ne marche pas, en fait. Ça c'est du tuto.

##Installation

Au niveau des détails auxquels on ne pense pas forcément mais qui sont importants :

* j'ai acheté un adaptateur secteur pour que l'appareil tourne non-stop toute la soirée ;
* j'ai prévu une carte SD de rechange.

Enfin, lors de l'installation dans la salle, j'ai activé le retardateur. Ainsi, quand on appuie, on a deux secondes pour faire le beau avant que ça parte. La salle étant assez sombre de nuit, le flash est activé. Ce qui donne un retour aux utilisateurs pour leur informer du fait que la photo est prise et qu'ils peuvent arrêter de tirer la langue.

Au niveau du décor, j'ai fait simple en posant des palettes sur le fond. Sur ces palettes, des accessoires pour que les gens aient un look pas possible.

## Réception critique

347 photos de prises, des gens qui avait l'air de se marrer, le résultat est positif. Reste qu'il y a eu pas mal de soucis qui ont demandé à 2-3 personnes de maintenir le dispositif en état de marche tout au long de la soirée, CF les paragraphes suivants.

L'évolution des photos au cours de la soirée est sympa à voir : ça commence plutôt sagement, avec des gens qui font des petits grimaces. Et ça finit en pogo, signes obscènes et yeux vitreux.

Effet positif inattendu : quelques enfants entre 7 et 10 ans se sont éclatés avec le truc. Ça a pu les occuper pendant la soirée. Sinon, ils se seraient surement ennuyés.

##Tenue de la charge

Lors de mes tests, j'avais bien veillé à appuyer très fort sur le bouton pour vérifier qu'il tiendrait le coup. Sauf que je n'avais pas anticipé un détail : les gens n'appuient pas fort, ils martèlent avec une violence sadique. Pire encore, les enfants qui sont trop petits s'accrochent au buzzer pour pouvoir grimper et actionner le bouton. Bref :

![](/images/buzzer/casse.jpg){.img-responsive}

Le buzzer a pris cher. Belle allégorie de la mise en ligne d'un site web mal optimisé qui croule sous le nombre de requêtes et qui plante. J'ai mal estimé la charge que mon bousin allait devoir encaisser, et j'ai perdu.


##Failles de sécurité

Un grand principe de base de la sécurité en web/informatique, c'est qu'il faut systématiquement contrôler les données venant de l'extérieur, l'input utilisateur.

Gros fail sur mon dispositif : l'appareil photo est resté accessible à tout le monde. Le beau Reflex Nikon, posé sur son trépied, visible de tous, avec son gros écran et ses 43 boutons. Du coup, les gens l'ont manipulé. Pourquoi ? Pour revoir les photos qu'ils avaient prises, ou encore pour changer des réglages. Ce dernier point mène à un autre énorme "POURQUOI ???", auquel je n'ai pas de réponse. Toujours est-il que l'appareil photo a été régulièrement tripoté, les réglages ont souvent été changés/annulés, et le cadrage a été mis à l'ouest. Là aussi il a fallu intervenir régulièrement sur l'appareil pour le remettre en ordre de marche. Il faut donc penser à déleguer la gestion de tout ça à quelqu'un.

Normallement je ne devrais pas me re-marier, mais si c'était à refaire, je rajouterais :

* un écriteau sur l'appareil photo expliquant qu'il faut aller se placer devant et juste appuyer sur le bouton ;
* un cache devant l'écran ;
* 6 pièges à loup électrifiés autour du trépied.

##Usages dérivés

Il reste le fait de laisser le pouvoir aux invités de prendre les poses qu'ils souhaitent. On sait déjà ce que ça donne [quand on permet aux gens de faire ce qu'ils veulent](http://www.dailymail.co.uk/femail/article-3243963/Nutella-personalised-labels-campaign-backfires-customers-share-pictures-jars-named-Diabetes-Vegemite-Hitler.html). Mais quand ça nous arrive à nous, c'est encore plus drôle :

![](/images/buzzer/resultat2.jpg){.img-responsive}

##La maintenance

C'est parti pour le parallèle à la con : un site web, ce n'est pas un produit fini qu'on livre en une fois et qui vit sa vie tranquillement tout seul comme un grand. Une fois que le site est déployé, il faut le maintenir en vie, même si en apparence rien ne change. C'est la même chose qu'avec le bouton à photos qui part en biberine tout au long de la soirée : il faut être à ses côtés pour le surveiller, pour intervenir en cas de problème, pour faire des ajustements une fois qu'on s'est confronté aux contraintes de la réalité.
