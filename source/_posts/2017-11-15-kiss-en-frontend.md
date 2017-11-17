---
title: Où est passé le KISS en développement front ?
tags:
    - Dev
    - Savoir vivre de dev

---

Je suis tombé en admiration devant ces deux tweets :
<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">do you ever stop and think, maybe people are over-thinking/engineering front-end development?</p>&mdash; Ben Howdle (@ben_howdle) <a href="https://twitter.com/ben_howdle/status/930012526628110337?ref_src=twsrc%5Etfw">November 13, 2017</a></blockquote>

<blockquote class="twitter-tweet" data-conversation="none" data-lang="fr"><p lang="en" dir="ltr">“Premature optimization is the root of all evil”, which we apply to everywhere but front-end development. We seem to start with an overly complex baseline and work up from there.</p>&mdash; Ben Howdle (@ben_howdle) <a href="https://twitter.com/ben_howdle/status/930153429007290368?ref_src=twsrc%5Etfw">13 novembre 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Troller l'écosystème Javascript sur Twitter, c'est facile et répandu. Mais ces deux tweets là ne tirent pas sur l'ambulance comme les autres. Ici on ne critique pas à quel point c'est complexe et moche. On se pose plutôt la question "*est-ce que cette complexité nous est tout le temps nécessaire ?*".

<!--more-->

J'ai pondu une interface un poil chiadée il y a quelques mois. Elle se trouve [ici](https://www.latoquante.com/fr_FR/watch/create).

![](/images/toquante_interface.png){.img-responsive}

Cette page permet de [personnaliser une montre](https://www.latoquante.com) en interchangeant ses différents composants. J'en suis plutôt fier au niveau ergonomie (ne parlons pas du design austère) car :

* ma spécialité c'est le back, le front n'est pas ma tasse de thé ;
* les tests utilisateurs ont été concluants ;
* on a reçu de bons commentaires de la part de "gens du métier" ;
* on a observé les utilisateurs et pissé de joie en les voyant se prendre au jeu de la personnalisation en jouant frénétiquement avec l'interface.

Les technos utilisées pour cette page : du [Javascript à la vanille](http://vanilla-js.com/) et quelques lignes de JQuery (pas forcément indispensables de surcroît). C'est moins sexy à dire que Du Coffee Script couplé à React et Ember compilé avec Gulp qui tourne sous Electron jantes alliages antenne chromée. Je fais du name dropping alors que si ça se trouve, la moitié de ces trucs est déjà has-been, j'en sais rien.

Et le plus horrible, dont je suis en plus fier : les assets sont compilés avec Assetic, le vieux bundle pas loin d'être déprécié pour Symfony2. Flemme absolue d'installer une stack Node ou un de ses 400 forks sur mes environnements de dev et déploiement, tout ça pour coller 3 fichiers ensemble et faire du rechercher/remplacer à certains endroits.

Je fais tous ces choix de vieux con car c'est infiniment plus simple pour moi. Pas besoin de stack JS à laquelle je ne comprends rien pour compiler mes assets. Au final, malgré la certaine complexité de la page, ça reste un pauvre écran qui affiche et cache des trucs quand on clique sur des machins. Je n'ai pas besoin d'un framework de déglingo pour ces pétouilles. **On est toujours sur un site web, pas une "application"**, chose qui a tendance à se perdre ces temps ci : on fait de l'application web à foison, de la Single Page App à gogo, tout ça pour consulter le programme TV ou la météo.

Un jour ma page migrera peut-être vers une stack JS plus musclée, pour des histoires de complexité de code et de maintenabilité, car ces outils sont évidemment intéressants dans certains cas. Mais j'espère que ça sera le plus tard possible, car à ce moment là, cette page deviendra lente :

<blockquote class="twitter-tweet" data-lang="fr"><p lang="en" dir="ltr">almost everything on computers is perceptually slower than it was in 1983</p>&mdash; Gravis! (@gravislizard) <a href="https://twitter.com/gravislizard/status/927593460642615296?ref_src=twsrc%5Etfw">6 novembre 2017</a></blockquote>

<blockquote class="twitter-tweet" data-conversation="none" data-lang="fr"><p lang="en" dir="ltr">amber-screen library computer in 1998: type in two words and hit F3. search results appear instantly.</p>&mdash; Gravis! (@gravislizard) <a href="https://twitter.com/gravislizard/status/927593804168753152?ref_src=twsrc%5Etfw">6 novembre 2017</a></blockquote>

<blockquote class="twitter-tweet" data-conversation="none" data-lang="fr"><p lang="en" dir="ltr">now: type in two words, wait for an AJAX popup. get a throbber for five seconds. oops you pressed a key, your results are erased</p>&mdash; Gravis! (@gravislizard) <a href="https://twitter.com/gravislizard/status/927593894325260288?ref_src=twsrc%5Etfw">6 novembre 2017</a></blockquote>

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

(et je recommande de lire la suite du thread)
