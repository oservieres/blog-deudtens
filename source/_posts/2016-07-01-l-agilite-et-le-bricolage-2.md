---
title: Un chariot à timelapse construit en Agile (1/2)
tags:
    - Savoir vivre de dev
    - Agile
    - Bidouillage

---

# Récapitulatif de l'épisode précédent

Si vous ne l'avez pas déjà fait, je vous conseille de lire le premier épisode. Sinon, en bref : je cherche à construire un truc, et la première version pleinement fonctionnelle est très décevante.

# Rétrospective

Mon rail fonctionne mal. Lorsque le chariot passe sur des jonctions, il bouge, et cela rend l'image instable.

Mais pire que ça, je me rends compte que j'ai construit un objet qui ne me sert à rien :
* ok, le rail fait 1m50, c'est super. Mais je me rends compte que je n'ai pas besoin d'autant de longueur. Le tiers de cela me suffit pour faire un petit travelling sympa.
* Le machin que j'ai construit est LOURD. Comme quand on développe une usine à gaz en informatique. On dit souvent que c'est lourd. Ben là c'est pareil, sauf que c'est littéralement lourd.

Bref, je me suis focalisé sur l'extensibilité alors que je n'en avais pas besoin. Je ne vais même pas chercher à régler ce problème de secousses sur les jonctions : je n'ai plus besoin des jonctions.

En disant ça, je fais quelque chose que j'ai trop peu vu dans ma vie de développeur : j'abandonne une fonctionnalité. J'aimerais que ça arrive plus souvent, mais il y a toujours une (mauvaise) raison pour garder cet écran de backend pourri qui plante constamment, ou bien cette recherche avancée que personne n'utilise.

Je retourne à Leroy Merlin acheter des profilés en fer beaucoup plus légers. Et je les coupe à la bonne longueur pile pour qu'ils rentrent dans ma plus grosse valise. Aussi, je rajoute une equerre entre mon rail et mon boitier moteur, afin de pouvoir séparer les deux facilement pour le voyage. Et hop :

Le résultat :


C'est beaucoup mieux ! Nouveau problème : mes nouveaux rails sont flexibles. Ils plient sous le poids du chariot et de l'appareil. Je décide de récupérer des élements de l'ancien rail pour consolider le tout :

Le résultat :

Ca commence a être vraiment bien. Au passage, j'ai réglé deux petits problèmes :

* Le fil avait tendance à mal s'enrouler autour du mandrin. Une pièce en plastique permet maintenant de guider le fil.
* La télécommande de l'appareil photo trainait, je l'ai fixée au boitier avec du velcro.


# Et après

Il y a un problème avec mon dispositif : le moteur tourne en continu, la caméra est en perpétuel mouvement. C'est une limitation qui provoque des symptômes lorsque l'on fait des expositions longues :

Bref, le mouvement combiné à l'exposition longue provoque du flou de mouvement.

D'un côté ça m'embête bien. mais d'un autre côté, ça couterait très cher de corriger ce point. Si un développeur et un chef de projet parlaient de ce problème, ça donnerait ça :

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

- Non, il faut quelque chose qui programme l'action du moteur à intervalles réguliers. Et puis il faut changer le moteur : il faut qu'il soit plus rapide pour rattraper la distance non parcourue quand la photo est en train d'être prise. Et il faut qu'il soit précis, donc il faudrait probablement passer à un moteur pas-à-pas.

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
* 
