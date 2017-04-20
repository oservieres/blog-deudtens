---
title: Déployez en production dès le début du projet !
tags:
    - Dev
    - Savoir vivre de dev

---

![](/images/deploy-meme.gif){.img-responsive}

En bref : quand vous vous lancez dans un nouveau projet (web ou autre), déployez le en production le plus vite possible, même si vous n'avez pas encore fait grand chose et que votre projet ne fait qu'afficher un message qui dit "caca pouet". Vous vous remercierez plus tard.

<!--more-->

## Premier exemple : la transcription en live pour les sourds au Mix-It

L'édition 2017 de la conférence Mix-It disposait d'un écran qui affichait la retranscription en temps réel des paroles du speaker. Le fonctionnement : un logiciel faisait de la reconnaissance vocale et écrivait approximativement ce qui était dit. Ensuite, un opérateur corrigeait en live le texte qui était affiché.

![](/images/velotype2.jpg){.img-responsive}

Ça, c'est en théorie. En pratique, l'outil était en bêta, et son utilisation à cet événement était surtout faite pour le tester. Et c'est une super idée, car le truc déconnait à mort ! J'ai été amusé (comme d'autres) de voir à quel point l'outil rencontrait des problèmes, dont certains ne pouvaient être décelables qu'avec ce genre de **test grandeur nature** :

* un problème de scroll empêchait de voir les dernières paroles retranscrites, ce qui donnait une grande latence entre paroles et texte ;
* la reconnaissance vocale était totalement peaumée dès que le speaker faisait du franglais ;
* une fenêtre TeamViewer trainait sur l'écran : ça sent le cafouillage à base de partage d'écran qui n'a pas été possible ;
* entre deux talks, quand les organisateurs discutaient à voix basse entre eux au pupitre, leur conversation inaudible était retranscrite à l'écran ;

Bref, l'outil a été utilisé et montré alors qu'il n'était pas du tout prêt, et je trouve ça extrêmement positif. J'aime à croire que son créateur a appris beaucoup de choses avec cette expérimentation, et qu'il n'aurait pas pu les déceler aussi tôt autrement. D'ailleurs, on voyait l'outil s'améliorer au fur et à mesure des conférences : avant la fin de la journée, le premier problème dont je parlais était réglé.

![](/images/velotype1.jpg){.img-responsive}

## Déployer en production sur le web

L'exemple précédent concerne un outil à usage local, mais j'écris cet article en pensant avant tout au web. Déployer son site en production dès le début, c'est bon pour la santé, et de plein de manières : au moins, c'est fait, on n'en parle plus, et vous ne pourrez plus arriver la gueule enfarinée une semaine avant l'ouverture du site en vous rendant compte que déployer en production en un click, en fait, c'est pas facile.

Au tout début, votre site est un bête "Hello World" qui est déployable via un tout aussi bête `scp` ou `rsync`. Ensuite, vous lui rajoutez une base de données, de la génération d'assets CSS/JS, du cache fichiers, et autres joyeusetés. La procédure de déploiement se complexifie. Il vaut mieux enrichir et/ou remanier sa procédure de déploiement au fur et à mesure plutôt que de tout se prendre sur le coin de la tronche le jour où on n'attend plus que vous pour mettre en ligne et gagner du pognon.

J'insiste sur le fait de déployer en production, et pas seulement en pré-production : la pré-production n'est jamais iso-prod, malgré ce qu'on voudrait faire croire. A commencer par le fait que généralement, la production est redondée/répliquée, et pas la pré-production, ce qui change beaucoup de choses.

Déployer en production très tôt, c'est la possibilité de casser notre site en toute impunité, sans stress, et en apprenant beaucoup au passage.

## Second exemple : La Toquante, mon projet personnel

![](/images/latoquante-prod.jpg){.img-responsive}

Je me suis associé avec une personne (où plutot : un entrepreneur m'a proposé de m'associer à lui) pour vendre des montres personnalisables. Tout ceci à l'aide d'un site web que je développe. La boutique n'est pas encore ouverte, mais le site est déjà en production depuis plusieurs mois, alors qu'il est pas fini/moche/buggé. Les prix des montres ne sont même pas les bons. Les images des produits sont foireuses. Et les contenus (CGV, page de présentation...) sont incomplets/erronnés. Mais on s'en cague, là n'est pas l'intérêt !

Question cruciale : **si le site est en production, comment le cacher du public tant qu'il n'est pas officiellement ouvert ?**

Dans mon cas, pour La Toquante, j'ai choisi une solution plutôt simple : j'ai rien fait. Le site est déjà accessible au public. il est déjà tout prêt, j'ai juste fait preuve de délicatesse sur deux points qui seront modifiés quelques jours avant l'ouverture :

* La page de paiement est en mode "test". Impossible de faire rentrer du vrai argent.
* J'ai empêché l'indexation du site sur les moteurs de recherche avec le fichier robots.txt.

Ainsi, je me fous pas mal que des gens aient accès au site, de toute façon ils ne savent pas qu'il se trouve à l'adresse [www.latoquante.com](https://www.latoquante.com). Ah, merde.

Deux raisons pour lesquelles le site est déjà ouvert au grand public :

* Flemme absolue de cacher le site, car c'est difficile à faire sans contraintes fortes.
* Je peux montrer le site à n'importe qui, n'importe où, sur n'importe quel device, juste en tapant l'adresse dans le navigateur. Car dès que j'ai une idée ou un truc à montrer, je saoule tout le monde avec. hors de question de garder des choses secrètes : personne n'ira vous piquer votre idée, car votre idée, tout le monde s'en fout et peu de gens y croient. Donc autant la pitcher à un maximum de monde pour amasser le plus de retours possible.

## Si on veut vraiment cacher son site

Car après tout, je suis conscient de la particularité de mon cas : on peut avoir de très bonnes raisons de vouloir cacher son site. Moi même, je manque encore de recul et peut-être qu'un jour je regretterai de ne pas l'avoir caché ! Plusieurs solutions, mais aucune n'est parfaite :

* Ne pas configurer le nom de domaine, et trifouiller son fichier `/etc/hosts`. Chiant pour tester sur des terminaux non configurés, chiant pour expliquer la manip' à un non dev, et impossible de tester les appels provenant de l'extérieur (callback de paiement en tête).
* Ajouter une authentification HTTP sur toutes les pages sauf callback de paiement : j'aime pas. Ça c'est de l'argumentation.
* Whitelister par IP. Les IP, ça change. Même quand elles sont fixes : je peux me connecter de plein d'endroits différents.
* Un mélange d'un peu tous les points précédents. J'ai envie de me flinguer rien que d'y penser.

## Le déploiement continu en vue

Déployer son site tôt, c'est s'assurer d'avoir une procédure de déploiement béton, et c'est un premier pas vers le déploiement continu.
