---
title: Interface web de personnalisation produit : quelles solutions ?
tags:
    - Dev

---

Retour sur cette interface de [personnalisation de montre](https://www.latoquante.com/fr_FR/watch/create_from_model/Golden%20leaves/55) que j'ai développée il y a quelques temps :
![](/images/toquante_interface.png){.img-responsive}

Un peu de contexte : je suis le co-fondateur du site [latoquante.com](https://www.latoquante.com). Le site permet de confectionner votre propre montre en choisissant les pièces qui la composent ainsi que le dessin créé par un artiste atypique qui va orner son cadran. La notion de personnalisation du produit est donc au centre de notre offre.

Le gros défi : arriver à prévisualiser la montre selon les modifications faites.

Cet article montre les différentes solutions que j'ai étudiées et/ou envisagées en allant voir les autres sites du genre.

<!--more-->

## Le besoin

Pouvoir confectionner sa propre montre en choisissant facilement les éléments suivants :

* monture ;
* bracelet ;
* couleur de fond du cadran ;
* dessin ;
* aiguilles.

On est sur la première version du site, à mettre en production rapidement avec une version minimale : il faut chercher la simplicité à tout prix. Deux axes de travail :

* effort de développement minimal ;
* possibilité dans l'interface d'aministration d'ajouter de nouvelles pièces/dessins facilement et rapidement.

## Chez BMW

[![](/images/personnalisation/bmw.jpg){.img-responsive}](http://www.bmw.fr/vc/ncc/xhtml/start/startWithConfigUrl.faces?country=FR&market=FR&productType=1&brand=BM&locale=fr_FR&name=w5s7c1p6#ExteriorMain)

Ca ressemble à de la 3D précalculée puis appliquée à des sprites 2D comme au temps des premiers jeux de course en trois dimensions : un modèle 3D est "photographié" sous tous les angles, puis un changement d'angle de la caméra affiche l'image 2D qui correspond. C'est une technique assez répandue, parfois aussi faite avec des vraies photos prises tout autour d'un sujet "physique".

C'est sympa, ça assure la compatibilité avec pas mal de navigateurs, et ça marche plutôt bien. Le seul problème, c'est qu'il faut précalculer toutes les combinaisons de montres possibles. Or, on en a une infinité (façon de parler). Pas envisageable dans mon cas, surtout qu'on va souvent rajouter de nouveaux dessins et pièces, ce qui demandera beauoup de recalculs. De plus, j'exclus du cahier des charges la possibilité de faire pivoter la montre : pour commencer, ce sera juste une vue de face, point.

## Chez Oh My Watch

[![](/images/personnalisation/montre.jpg){.img-responsive}](https://www.ohmywatch.fr/toutes-nos-montres/montres-personnalisees/montre-personnalisee-classic-by-ohmywatch.php)

Intéressant : ça joue sur des PNG qui s'empilent les uns sur les autres, avec de la transparence.

![](/images/personnalisation/ohmywatch2.png){.img-responsive}

Par contre, le site a un autre positionnement que le notre : il donne une totale liberté sur le cadran (ajout de photo personnelle, texte, etc.), et restreint les personalisations du reste de la montre. On fait à peu près l'inverse : la plupart des pièces de nos montres sont interchangeables, mais le choix des dessins du cadran est fixé et restreint, pour assurer une identité à notre marque. Ce positionnement m'arrange : rajouter un mini éditeur WYSIWIG au milieu de la montre avec déplacement et redimensionnement des éléments, c'est trop compliqué ! Or de question de devoir gérer le positionnement d'éléments avec des coordonnées à stocker quelque part, je veux quelque chose de beaucoup plus bête.

## Chez Renault

[![](/images/personnalisation/renault.jpg){.img-responsive}](https://conf.renault.fr/disco/zoe?modelKey=W10&criteriaUri=SRV%24MMCOYOTE%2FTERQG&versionUri=&obsolescence=1&confUri=http%3A%2F%2Fpgr-fr.co.rplug.renault.com%2Fc%2FBACcz%2FAJYo8%3Bpc%3DAxK%23this&choiceMode=off#this)

Oh, c'est joli ! Oh, c'est en Flash ! AU REVOIR !

## Chez Like A Color

[![](/images/personnalisation/meubles.jpg){.img-responsive}](https://www.likeacolor.com/fr/stickers-decoratifs-ikea/232-stickers-pour-1-tiroir-caisson-vika-alex-.html)

Alors eux ce sont mes champions. La photo du meuble est un PNG avec transparence. La partie colorée en rouge est en fait transparente. Et il y a un DIV sous l'image qui a une couleur de fond qui varie selon ce que l'utilisateur sélectionne. C'est génialement débile, j'adore ! C'est ce genre de mentalité que je veux avoir pour développer mon interface.

NB : depuis ma phase de recherches, il semblerait que ce mode de fonctionnement ne soit plus d'actualité. Le serveur renvoie des images toutes faites maintenant.

## Threekit

[![](/images/personnalisation/threekit.png){.img-responsive}](https://threekit.com/)

Une solution technique qui fournit exactement ce que je veux faire en 3D. Je préfèrerai investir dans du temps de développement plutôt que dans l'achat de cette brique, sachant que je suis sur un projet parallèle à mon activité professionnelle et que je n'ai que du temps à investir, pas de l'argent.

## Solution retenue

Je suis allé au plus simple : j'empile des PNG qui ont tous la même taille et dont tous les éléments sont déjà bien positionnés pour s'aligner les uns sur les autres.

![](/images/personnalisation/breakdown.jpg){.img-responsive}

L'empilage des différentes couches est fait côté client. Par contre, j'ai besoin d'assembler les couches à d'autres endroits :

* dans l'interface d'administration : j'empile dessin et fond de cadran sur un gros fichier JPG pour rendre le tout imprimable.
* dans l'envoi d'email de confirmation de commande ou de relance après un panier abandonné : j'affiche la montre dans le corps de l'email. Cela demande donc d'avoir une image en JPG d'un seul tenant.

![](/images/personnalisation/mail.png){.img-responsive}

Les modèles homme et femme des montres ont des tailles différentes. Mais ça m'ennuie de dupliquer les visuels des dessins et fonds de cadrans juste pour une petite différence de taille. Ainsi, je mets toutes les montres à la même taille, et je fais varier leur taille à l'affichage dans le navigateur.

Cette technique pourrait permettre d'afficher une vue de côté de la montre, en associant une deuxième image à chaque pièce. Mais on commence simple : pour l'instant, on s'en passe.

## Et pour plus tard ?

Je suis assez tenté par du WebGL comme ce que fait Threekit, avec du fallback sur ma solution originale à base de PNG en cas de besoin. La modélisation en 3D ne me fait pas peur : au final, on ajoute souvent de nouveaux dessins, mais moins souvent de nouveaux éléments comme les montures et les bracelets. Ce serait l'occasion de tester [Three.js](https://threejs.org/), qui semble être la bibliothèque utilisée par Threekit justement. Mais pour l'instant on n'en est pas là : on a une première version du site qui fonctionne. Il nous faut maintenant du recul sur nos premiers mois d'activités avant de d'envisager ce genre d'évolution majeure.
