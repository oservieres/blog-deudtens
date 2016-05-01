---
title: J'adore coder sans specifications
tags:
    - Savoir vivre de dev

---

Explication pour les profanes : normalement, quand on demande à une développeur de développer, on lui donne notre besoin précis. Des spécifications. Souvent, le développeur n'arrive pas à obtenir ces spécifications. Et généralement, ça l'énerve.

<!--more-->

Quand je n'arrive pas à obtenir de specs pour un développement que je dois réaliser, je suis heureux : ça veut dire que je peux faire ce que je veux !

Premier exemple concret : internationaliser un site web existant. J'ai vécu ce besoin trois fois. A chaque fois, les mêmes questions reviennent :

* Dans quels pays veut-on apparaitre pour commencer ? Et ensuite ?
* Comment gère-t-on les langues ? On en garde une seule ? Une langue par pays ? Plusieurs par pays ? On décorelle la langue du pays ?
* Mêmes questions pour les devises.
* Mêmes questions pour les taxes/TVA. En plus, certains pays en appliquent plusieurs, non ?
* Est-ce qu'on utilise un compte en banque spécifique à chaque pays ?
* Est-ce qu'on cloisonne les clients/utilisateurs par pays ?
* Un utilisateur peut-il changer de pays ? 
* Est-ce qu'un utilisateur du site français peut fournir une adresse de domicile dans un autre pays ?
* Que veut-on comme noms de domaines et routes ? Un nom de domaine par pays ? Une locale en préfixe de chaque route ?
* Dans quelle devise envoie-t-on nos rapports de ventes à nos partenaires/fournisseurs ?
* Comment fait-on pour calculer des statistiques de ventes si on les réalise dans plusieurs devises différentes ?
* On doit convertir des prix dans d'autres devises ? En utilisant quel taux ? On convertit au moment de la commande ou bien plus tard ?
* ...

Il n'y a pas de réponse unique à ces questions. Tout dépend du produit, du contexte, de la société.

Au final, le besoin business il se fout de pas mal de ces questions au début. Lui, il stipule juste "je veux vendre mes articles en Allemagne et en Suisse".

De mon expérience, c'est généralement le développeur qui demande des eclaircissements sur ces points. Le fonctionnel saura répondre rapidement au premier tiers de ces questions. Il répondra avec réflexion au deuxième tiers. Il répondra puis se contredira à maintes reprises sur le troisième tiers. Et enfin, il ne saura pas du tout répondre au dernier tiers.

Oui, ça fait quatre tiers. [Mais tout dépend de la taille des tiers, c'est Marcel Pagnol qui le dit](http://www.marcel-pagnol.com/biblio-marius,8.html).

Bref, le développeur est  livré à lui même concernant deux petits tiers (qu'on peut arrondire à la moitié, c'est bon vous suivez ?) des questions qui le taraudent. Généralement, c'est là que la dépression commence. Personnellement, ça m'excite pas mal. C'est le moment où je peux sortir de mon quotidien de pissage de code pour aller parler avec des vrais gens et leur soumettre des idées (qui généralement me font faire le moins de développement possible).
