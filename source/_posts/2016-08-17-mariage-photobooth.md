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

##La solution

Mettre à disposition des convives un énorme bouton rouge qui déclenche une photo lorsqu'on appuie dessus. Un gros bouton comme ça, ça serait cool :

![](/images/buzzer/modele.jpg){.img-responsive}

Joie, j'ai trouvé exactement ce modèle sur le net, que j'ai collé en haut d'un socle fait avec des matériaux de récupération. Il trône ici au milieu de tout le bordel de décoration du mariage :

![](/images/buzzer/preparation.jpg){.img-responsive}

Notez que le socle est très haut. Pour éviter que les enfants ne s'excitent sur le bouton. A ce moment là, je me crois encore malin en pensant que ça va les arrêter.

##Fabrication

Ma première idée, c'était de trifouiller une télécommande infra-rouge, pour remplacer son bouton par mon gros bouton rouge. Mauvaise idée. Version courte : ça marche pas. Sombre histoire de soudures qui ne tiennent pas sur le circuit imprimé de la télécommande.

L'idée retenue au final, ça a été d'utiliser le bouton comme grosse télécommande filaire. L'appareil étant un Nikon, j'ai du acheter un cable de télécommande qui a un embout propriétaire ainsi qu'une rallonge de 5m. Il me restait donc à raccorder l'autre côté du cable à l'interrupteur, ce qui se fait facilement une fois qu'on a trouvé quels fils raccorder à quelles bornes en essayant les combinaisons une par une. Attention : il y a une combinaison qui marche presque, mais qui ne marche pas, en fait. Ça c'est du tuto.

Au niveau des détails auxquels on ne pense pas forcément mais qui sont importants :

* j'ai acheté un adaptateur secteur pour que l'appareil tourne non-stop toute la soirée ;
* j'ai prévu une carte SD de rechange.

Enfin, lors de l'installation dans la salle, j'ai activé le retardateur. Ainsi, quand on appuie, on a deux secondes pour faire le beau avant que ça parte. La salle étant assez sombre de nuit, le flash est activé. Ce qui donne un retour aux utilisateurs pour leur informer du fait que la photo est prise et qu'ils peuvent arrêter de tirer la langue.

## Réception critique

Quelques centaines de photos de prises, des gens qui avait l'air de se marrer, le résultat est positif. Reste qu'il y a eu pas mal de soucis qui ont demandé à 2-3 personnes de maintenir le dispositif en état de marche tout au long de la soirée, CF les paragraphes suivants.

##Tenue de la charge

Lors de mes tests, j'avais bien veillé à appuyer très fort sur le bouton pour vérifier qu'il tiendrait le coup. Sauf que je n'avais pas anticipé un détail : les gens n'appuient pas fort, ils martèlent avec une violence sadique. Pire encore, les enfants qui sont trop petits s'accrochent au buzzer pour pouvoir grimper et actionner le bouton. Bref :

![](/images/buzzer/casse.jpg){.img-responsive}

Le buzzer a pris cher. Belle allégorie de la mise en ligne d'un site web mal optimisé qui croule sous le nombre de requêtes et qui plante. J'ai mal estimé la charge que mon bousin allait devoir encaisser, et j'ai perdu.


##Failles de sécurité

Un grand principe de base de la sécurité en web/informatique, c'est qu'il faut systématiquement contrôler les données venant de l'extérieur, l'input utilisateur. Gros fail sur mon dispositif : l'appareil photo est resté accessible à tout le monde. Le beau Reflex Nikon, posé sur son trépied, visible de tous, avec son gros écran et ses 43 boutons. Du coup, les gens l'ont manipulé. Pourquoi ? Pour revoir les photos qu'ils avaient prises, ou encore pour changer des réglages. Ce dernier point mène à un autre énorme "POURQUOI ???", mais bref. Toujours est-il que l'appareil photo a été régulièrement tripoté, les réglages ont souvent été changés/annulés, et le cadrage a été mis à l'ouest. Là aussi il a fallu intervenir régulièrement sur l'appareil pour le remettre en ordre de marche.

Bon, normallement je ne devrais pas me re-marier, mais si c'était à refaire, je rajouterais :

* un écriteau sur l'appareil photo expliquant qu'il faut aller se placer devant et juste appuyer sur le bouton ;
* un cache devant l'écran ;
* 6 pièges à loup électrifiés autour du trépied.

##Usages dérivés

Il reste le fait de laisser le pouvoir aux invités de prendre les poses qu'ils souhaitent. On sait déjà ce que ça donne [quand on permet aux gens de faire ce qu'ils veulent](http://www.dailymail.co.uk/femail/article-3243963/Nutella-personalised-labels-campaign-backfires-customers-share-pictures-jars-named-Diabetes-Vegemite-Hitler.html). Mais quand ça nous arrive à nous, c'est encore plus drôle :

![](/images/buzzer/resultat2.jpg){.img-responsive}

##La maintenance

Un site web, ce n'est pas un produit fini qu'on livre en une fois et qui vit sa vie tranquillement tout seul comme un grand. Une fois que le site est déployé, il faut le maintenir en vie, même si en apparence rien ne change. C'est la même chose qu'avec le bouton qui part en biberine tout au long de la soirée : il faut être à ses côtés pour le surveiller, pour intervenir en cas de problème, pour faire des ajustements une fois qu'on s'est confronté aux contraintes de la réalité.
