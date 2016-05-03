---
title: J'adore coder sans spécifications
tags:
    - Savoir vivre de dev

---

Explication pour les profanes : normalement, quand on demande à un/une développeur(se) de développer, on lui donne notre besoin précis. Des spécifications. Souvent, il/elle n'arrive pas à obtenir ces spécifications. Et généralement, ça l'énerve.

![](/images/no-idea-what-im-doing-2.jpg){.img-responsive}

<!--more-->

Quand je n'arrive pas à obtenir de specs pour un développement que je dois réaliser, je suis heureux : ça veut dire que je peux faire "ce que je veux" !

Cet article a été écrit dans mon contexte de salarié de start-up éditrice de solutions. Je n'ai jamais travaillé en SSII ou en agence web, pour lesquelles le contexte est potentiellement différent.

#Need ze no, to win, again, ze no

![](/images/needzeno.jpg){.img-responsive}

Premier exemple concret : internationaliser un site web existant. J'ai vécu ce besoin trois fois. A chaque fois, les mêmes questions reviennent :

* Dans quels pays veut-on apparaitre pour commencer ? Et ensuite ?
* Comment gère-t-on les langues ? On en garde une seule ? Une langue par pays ? Plusieurs par pays ? On décorelle la langue du pays ?
* Mêmes questions pour les devises.
* Mêmes questions pour les taxes/TVA. En plus, certains pays en appliquent plusieurs, non ?
* Est-ce qu'on utilise un compte en banque spécifique à chaque pays ?
* Est-ce qu'on cloisonne les clients/utilisateurs par pays ?
* Un utilisateur peut-il changer de pays ?
* Est-ce qu'un utilisateur du site français peut fournir une adresse de domicile dans un autre pays ?
* Que veut-on comme noms de domaines et routes ? Un nom de domaine par pays ? Une locale en préfixe de chaque route ? Est-ce qu'on traduit les routes ?
* Dans quelle devise envoie-t-on nos rapports de ventes à nos partenaires/fournisseurs ?
* Comment fait-on pour calculer des statistiques de ventes si on les réalise dans plusieurs devises différentes ?
* On doit convertir des prix dans d'autres devises ? En utilisant quel taux ? On convertit au moment de la commande ou bien plus tard ?
* ...

Il n'y a pas de réponse unique à ces questions. Tout dépend du produit, du contexte, de la société, et aussi un peu de ce qui arrange les développeurs.

![](/images/context.jpg){.img-responsive}

Le besoin business il se fout de pas mal de ces questions au début (et un peu aussi à la fin, pour certaines). Lui, il stipule juste "je veux vendre mes articles en Allemagne et en Suisse".

De mon expérience, c'est généralement le développeur qui demande des eclaircissements sur ces points. Le fonctionnel saura répondre rapidement au premier tiers de ces questions. Il répondra avec réflexion au deuxième tiers. Il répondra puis se contredira à maintes reprises sur le troisième tiers. Et enfin, il ne saura pas du tout répondre au dernier tiers.

Oui, ça fait quatre tiers. [Mais tout dépend de la taille des tiers, c'est Marcel Pagnol qui le dit](http://www.marcel-pagnol.com/biblio-marius,8.html).

Bref, le développeur est  livré à lui même concernant deux petits tiers (qu'on peut arrondir à la moitié, c'est bon vous suivez ?) des questions qui le taraudent. Généralement, c'est là que la dépression commence. Personnellement, ça m'excite pas mal. C'est le moment où je peux sortir de mon quotidien de pissage de code pour aller parler avec des vrais gens et leur soumettre des idées (qui généralement me font faire le moins de développement possible).

Pour moi la solution réside dans l'usage de ces trois trucs :

* l'agilité, pour avancer par itérations et réajuster la cible au fur et à mesure ;
* le déploiement continu, pour déployer vite, rapidement et sans stress ;
* le feature toggle, pour déployer des trucs pas finis en limitant leur visibilité par les clients.

On ne sait pas trop où viser ? Et bien on va essayer un truc, le déployer rapidement , analyser, corriger le tir, et recommencer. On retrouve très vaguement le principe du [Lean](http://www.infoq.com/fr/presentations/lean-startup-autour-petite-mousse).

Généralement, on a beau discuter d'un besoin avec un fonctionnel, au bout de quelques dizaines de minutes de dialogue, tout est devenu trop abstrait pour qu'on se comprenne. Le développeur a le code en tête, il voit exactement ce qu'il peut faire. Mais le fonctionnel est dans le flou total (sans forcément s'en rendre compte). Le fait de **faire un truc**, aussi petit soit-il, permet de montrer quelque chose au fonctionnel de tangible, pour qu'il prenne ses repères et qu'il visualise mieux une problématique afin de définir la prochaine étape.

"Faire un truc" peut revenir à faire un prototype. Par exemple, générer à la main un fichier CSV bidon si l'on doit développer des exports de vente. Je trouve que c'est un bon début, ça permet de cadrer certaines questions, mais que cela ne reste qu'une phase préliminaire. A un moment, il va falloir coder des trucs.

Tout mon article peut se résumer par cette magnifique vidéo :

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZXsQAXx_ao0" frameborder="0" allowfullscreen></iframe>

On a juste à faire plutôt que de discuter pendant des heures. Ainsi, on procède par petites étapes, on essaie différentes choses, on tatonne. Parfois on fait fausse route, on doit reculer et retirer du code. Deuxième étape de la démoralisation du développeur : modifier/virer des trucs qu'il vient de faire. Personnellement, [je m'en cague](http://www.dico2rue.com/dictionnaire/mot/25/s-en-caguer). Je suis payé pour faire tout ça, et il est convenu avec le fonctionnel que l'on avance ainsi. C'est le jeu.

Là ou ça devient un poil lourd, c'est quand il faut modifier la base de données. Du code, ça s'ajoute et se retire à volonté sans problème. La base de données par contre, elle se manipule avec précaution. Il faut utiliser un système de migrations robuste, et tenir compte de toutes ces difficultés :
* Modifier une grosse table, ça la vérouille et rend donc le site potentiellement indisponible pendant plusieurs secondes/minutes.
* Pour renommer un champ en toute sécurité, il vaut mieux parfois en créer une copie à côté et effacer l'ancien plusieurs heures après.
* Dès qu'on joue beaucoup avec les migrations, il devient difficile de travailler à plusieurs en parallèle sur le projet sans avoir de collisions.

Difficile sous ces conditions d'y aller totalement en mode YOLO et tenter des trucs à foison.

#Pimp my site

![](/images/ugly-site.jpg){.img-responsive}

Second exemple : le site corpo d'une société éditrice. C'est généralement très vieux et moche. On se dit constamment qu'on devrait l'améliorer mais ce n'est jamais prioritaire, ça passe toujours après des développements qui ont une valeur à court terme. Et puis surtout, on ne sait pas ce qu'on veut. On veut un truc plus joli, voilà.

Avertissement : je n'ai jamais bossé en agence web. Ce qui va suivre va peut-être en défriser certains.

J'ai déjà vécu un un moment d'interblocage. Plusieurs personnes étaient motivées pour travailler sur le nouveau site corpo en donnant un peu de leur temps libre, mais chacun attendait de l'input des autres. En schématisant un peu, ça donnait ça :

* on voulait acheter un thème wordpress tout fait mais on attendait de savoir quel contenu mettre pour orienter le choix ;
* on voulait produire du contenu mais on mettait des plombes à formuler la moindre phrase et on attendait d'avoir une idée de ce que les développeurs pouvaient fournir comme mise en page ;
* les développeurs attendaient que le choix du thème soit fait pour donner leur avis sur les possibilités de mise en page des articles.

![](/images/cat-tail.gif){.img-responsive}

Ca m'a personnellement donné des boutons, cette volonté de sortir un truc [nickel chrome](https://fr.wiktionary.org/wiki/nickel_chrome) dès le début, à un point où on ne sort rien.

Au final, on est sorti de ce cercle vicieux en prenant deux décisions :

* quelqu'un écrit très rapidement les grandes lignes du contenu qu'il faut mettre, classé par pages ;
* on balance ce contenu tout dégueulasse sur un wordpress tout frais avec le thème de base (twentysixteen pour l'occasion).

A partir de là, on a pu partir sur des itérations. Rien que le fait de voir un site tout pourri utilisable a permis aux fonctionnels de faire avancer leur réflexion sur le contenu et comment l'organiser. Même chose pour le visuel : le fait de montrer un résultat moche stimule l'envie de nous donner des retours/directives.

Nous avons demandé aux fonctionnels "donnez nous l'adresse d'un site qui vous plait et auquel vous voudriez ressembler". 2 jours après avoir modifié le design en accord avec la réponse, on nous fournissait un autre site de référence qui n'avait rien à voir. Tout détruire pour tout recommencer. Ca fait mal au début, mais on s'y fait. Et au final, les gens sont contents.

Le pair programming a aidé, mais en combinant un développeur avec un fonctionnel. Même de manière sporadique, pendant 10 minutes par-ci par-là. Un site corpo, c'est beaucoup plus simple que des questions d'internationalisation. Le développeur peut rapidement faire des modifications cosmétiques pour que le fonctionnel donne son feedback et ses précisions instantannément. J'aurais par contre personnellement plus de mal à préconniser la méthode pour des développements compliqués, qui demandent une vraie concentration de la part du développeur qui va cracher du code imbitable pour le fonctionnel qui va surchauffer à côté.

Enfin, il faut forcer à mettre en production. Sinon, ça n'arrive jamais. Il y a toujours quelque chose à finir. J'ai personnellement joué le névrotique en menaçant régulièrement de mettre le site en production à tout moment en demandant "j'ai le doigt sur la détente là, dites moi ce qui vous choque vraiment pour que je n'appuie pas, car ça va péter, ça vient !". C'est ma façon diplomate de demander aux gens de dissocier leurs besoins impératifs de ceux qui relèvent de la zone de confort, qui peuvent être traités après mise en production.

Je n'ai pas assisté à la phase finale de la MEP : fidèle à mon habitude depuis 2 ans, je prends mes congés pile au moment où l'on déploie. Pur hasard. A moins que mes collègues attendent que je m'en aille pour faire les choses importantes.

# Conclusion

Coder sans specs ne me met pas de mauvaise humeur. Au moment où ça commence à m'énerver, je me rappelle que je continue à faire mon job normallement, que je continue à faire avancer ma boite, et que je reste payé pour ça. Comme dans un précédent article, [je me résigne tranquillement](/je-ne-dis-jamais-non#se-r%C3%A9signer).
