---
title: Apprendre unity rapidement
tags:
    - dev jeu vidéo

---

"*J'aimerais bien me mettre à Unity pour rigoler, mais j'ai pas le temps, faudrait que j'arrive à me concentrer plus de 10 minutes d'affilée*". Si comme moi vous vous êtes dit ça, j'ai la solution ! Sauf si vous avez des enfants, là je ne réponds de rien.

![](/images/unity-cartaclysm.jpg){.img-responsive}

<!--more-->

Je me suis mis récemment à Unity pour développer un POC de jeu dont on peut suivre l'avancée sur twitter avec le croisillon [#CARTACLYSM](https://twitter.com/search?f=tweets&vertical=default&q=%23cartaclysm).

Je ferai plus tard un article sur ce projet en particulier. Ici, je veux surtout parler de comment rapidement s'amuser avec Unity comme je l'ai fait.

# Les tutoriaux obligatoires

Allez ici et suivez ces tutoriaux jusqu'au 3.2 inclus : [Faire rouler une boulette](https://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). Ce sont des tutoriaux vidéo. ATTENDEZ REVENEZ ! Moi non plus j'aime pas les tutoriaux vidéos, mais ceux là sont géniaux. Le rythme est parfait, les explications sont claires, il y a même des annotations en cas de zones de flou.

Suivez bien ces tutoriaux à la lettre, tranquillement. Ne sautez pas d'étapes en vous croyant malin, sinon ça fait le même résultat qu'avec les meubles Ikéa quand on prend la confiance.

En tout, vous en aurez pour 90 minutes (120 maximum). Ces vidéos vont vous permettre de comprendre les bases du fonctionnement d'Unity et de son interface. Je vous conseille de faire tout cela d'une traite si possible. Ca sera le seul moment où vous devrez vous concentrer pendant un si grand laps de temps.

Autre possibilité : regardez ces vidéos entre midi et 2 au boulot, même si vous n'avez pas l'éditeur à côté de vous. Et le soir, repassez-les vous en réalisant les opérations pour de bon.

# Les tutoriaux pour enfoncer le clou

Après les tutoriaux précédents, on a des bases, mais il manque un peu de savoir sur l'aspect "programmatique" : on sait créer des objets à la main dans l'éditeur avec du drag'n drop, mais comment les instancier de manière plus dynamique, au travers du code ?

La solution, c'est de se farcir ces tutoriaux jusqu'au 2.1 inclus : [Space Shooter](https://unity3d.com/learn/tutorials/projects/space-shooter-tutorial). Vous pouvez suivre les vidéos de manière un peu distraite jusqu'au 1.5 inclus. Je vous conseille de bien les écouter, car de bonne pratiques y sont révélées, mais si vous êtes pressé(e), vous pouvez faire des avances rapides.

A partir de ce moment, vous devriez avoir pigé pas mal de choses. Si vous souhaitez gagner un peu plus en assurance, je vous conseille les vidéos 2.2 à 2.5 : ne réalisez pas forcément les développements, contentez vous de regarder les vidéos.

# Le grand saut

C'est après avoir suivi les deux étapes précédentes que j'ai pu me lancer sur mon projet perso. Lorsque j'avais une question, j'ai trouvé ma réponse à ces endroits :

* [Google](https://www.google.fr)
* [Answers](http://answers.unity3d.com/) (Google y renvoie souvent)
* [Les Topics (en bas de page)](https://unity3d.com/learn/tutorials)

# Des conseils en vrac

Pour débuter, oubliez certains sujets comme l'interface et le son (ce sont les chapitres que je vous ai précédemment conseillés de scotomiser). Ce sont des sujets chiants et/ou compliqués et qui ne sont pas nécessaires pour débuter. Alors oui, le son c'est important, et il faut s'en occuper au fur et à mesure du développement sous peine d'accumuler une dette monstrueuse, mais on cherche à se former pour l'instant. Et dans mon cas personnel, mon POC n'a pas besoin de son pour que l'on vérifie sa pertinence.

Unity fournit des assets officiels qui permettent d'obtenir rapidement des objets déjà fonctionnels : système de vue FPS, véhicules, etc. Abusez-en ! Ils ne seront probablement pas dans votre jeu final, mais ils vous permettront de commencer votre projet rapidement en vous concentrant sur les spécificités de votre jeu.

Unity dispose aussi d'un asset store qui permet aux quidams de mettre à disposition leurs créations (modèles 3D, scripts, etc.), de manière payante ou gratuite. Abusez des assets gratuits pour votre POC ! Et n'achetez rien. La tentation de lâcher quelques dizaines de dollars pour ce module qui nous fait rêver est grande, après tout, ce n'est que 40 boules pour un truc super utile qui va me faire gagner du temps. Sauf qu'on va se dire ça pour plein d'articles différents, et que la facture va enfler de manière disproportionnée. De plus, ces assets ne sont en fait pas indispensables. Il est tout à fait possible d'avancer son projet sans eux.

La gestion des contrôles est assez fastidieuse : en gros, Unity ne propose pas de solution toute faite de base. Si votre jeu se joue seulement au clavier, ça va. S'il peut se jouer au clavier et à la manette, faut réfléchir un peu. S'il peut en plus se jouer sur plusieurs plateformes différentes, on commence à saigner du nez. S'il peut en plus se jouer à plusieurs joueurs sur la même machine, on fait un AVC. Commencez simple et réduisez votre périmètre de compatibilité. Même les plus gros en chient avec cette problématique, ce n'est pas pour rien.

Evitez de réfléchir trop "bas niveau" : je m'attendais à devoir faire de savants calculs trigonométriques pour placer mes objets. En fait, Unity fournit plein de machins dans son API pour abstraire les aspects les plus tordus de la programmation d'un jeu.
