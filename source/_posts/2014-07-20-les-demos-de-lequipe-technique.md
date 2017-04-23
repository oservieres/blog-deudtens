---
title: Les démos de l’équipe technique
tags:
    - Savoir vivre de dev

---

![](/images/demo1.jpg){.img-responsive}

Je suis sûr de moi quand je dis qu’il faut faire des démos régulières de ce que l’équipe de développement produit, qu’on soit en Scrum ou pas, Agile ou pas Agile. Sur le comment, je le suis un peu moins.


<!--more-->

##A quels intervalles ?

Evidemment en fin de sprint pour du Scrum. Sinon, toutes les 2 à 4 semaines je dirais. Le principal est de le faire à intervalles de temps très réguliers. Evènement récurent programmé dans le calendrier commun, et tout le monde est au courant.

##Qui y assiste ?

Ma vision du bouzin :

![](/images/demo2.jpg){.img-responsive}

* un animateur est désigné parmi les développeurs (on change à chaque fois) pour préparer et animer la démo ;
* le PO (ou le chef de projet) est le premier client de la démo. C’est à lui qu’on la fait, c’est son approbation et son bonheur absolu que l’on recherche. Et ses retours sont prioritaires. La démo commence quand le PO est là, tous les autres peuvent arriver au fil de l’eau ;
* tous les développeurs de l’équipe assistent à la démo. Ils n’y participent pas activement, sauf si l’animateur leur donne la parole sur un point technique spécifique. Ceci afin d’éviter le cas classique du fonctionnel qui pose une question en l’air, et de toute l’équipe technique qui lui répond différemment au même moment ;
* les spectateurs sont là car ils ont vu de la lumière. De manière générale, je suis pour inviter le plus de monde possible, et chacun sait s’il a un intérêt à venir assister au show ou pas. Mais ça peut dépendre des tailles et organisations des boites.


##Comment ça se passe ?

Bien. Séparer la phase effective de démo de l’étape des questions/réponses : l’animateur a une histoire à raconter, il ne doit pas être interrompu par une question business, une idée de génie qu’un spectateur vient d’avoir, là, comme ça. Bien faire comprendre aux spectateurs qu’ils notent leurs questions pour les poser à la fin et pas pendant la présentation.

C’est le plus compliqué du job : vous allez demander aux spectateurs d’attendre avant de poser les questions. Mais ils vont oublier et vous interrompre. Vous allez alors leur expliquer l’intérêt d’attendre, que leur questios est intéressante mais que vous n’y répondrez pas tout de suite. Eux vont entendre « Ta gueule ! » (oui, en gras et tout) et être tristes.

Et les gens oublient : les règles doivent être rappelées à chaque démo.

Si tout va bien, en appliquant cette méthode de manière stricte, vous serez catalogué dictateur nazi. Mais vous assurerez une démo courte, rythmée, qui a du punch (pas la boisson, enfin si vous voulez, pourquoi pas), et qui facilite la phase des questions : les moins importantes sont déjà oubliées par ceux qui voulaient les formuler, les plus intéressantes restent.

Pendant la phase de questions/réponses, l’animateur reste à son poste et doit cadrer les débats : le PO en priorité lui pose les questions, puis les spectateurs dans un second temps. C’est lui qui y répond ou qui choisit de donner la parole à un de ses comparses plus à même de répondre sur un sujet particulier. Sinon, pour toujours plus de fun, je vous conseille de jouer à « l’équipe de dev n’a pas le droit de parler » : l’animateur doit avoir assimilé les développements de tout le monde, doit pouvoir les présenter et les expliquer. Il est seul devant l’audience et doit répondre avec les informations dont il dispose, quitte à ce qu’il dise « je ne sais pas » sur les aspects les plus pointus.

J’aime rendre la phase de questions optionnelle : chacun est libre de se barrer une fois la démo terminée. Je me souviens d’un designer qui venait vérifier que l’on avait bien intégré ses maquettes. Peu intéressé par les questions fonctionnelles/business, il veillait à ce que l’on ait respecté ses directives. Il prenait ses notes, et partait en courant dès la démo terminée. Le temps que l’on sorte de la salle, nous avions reçu ses retours dans notre boite mail. Quand un truc aussi fluide se passe, c’est assez jouissif.

##Combien de temps ça dure ?

Entre 5 et 15 minutes pour la démo, puis 20 minutes max de questions/réponses. Pour rendre l’invitation sexy et donner envie aux gens de venir, 30 minutes de durée totale maximum me semble être un bon argument de vente.

##Comment on la prépare ?

La demi-journée précédant la démo, l’animateur la prépare en rédigeant son scénario. La rédaction du document est débile-compatible : elle décrit chaque étape à la manière de tests fonctionnels (Behat ou équivalents). Ainsi, le présentateur n’a plus qu’à suivre les instruction bêtement lorsqu’il déroule le script pour se concentrer sur sa prestation, son speech et son sex-appeal.

Le préparateur imprime son script, et ne le consulte pas sur son PC lors de la démo : il y a des chances qu’il finisse sur l’écran que tout le monde regarde, et c’est parfait pour déconcentrer l’audience.

J’aime bien envoyer un mail de rappel une demi-journée auparavant, en donnant la liste des fonctionnalités qui vont être démontrées.

##Comment on démontre des trucs « techniques » ?

J’ai longtemps pensé qu’on limitait la démo à ce qui était purement fonctionnel et qu’on occultait totalement les développement techniques. Mais il faut arriver à démontrer ces réalisations, sans endormir violemment l’audience. Et là je n’ai pas de recette miracle, il faut arriver à trouver une ruse différente pour chaque cas.

Une API REST à démontrer ? Plutôt que de montrer des appels curl qui ne parlent à personne, on peut cracher rapidement un mini client qui affiche les résultats en html. On peut aussi prendre 10 secondes pour faire dérouler les tests automatisés en montrant qu’il y a du vert partout et que c’est génial. Et expliquer pourquoi ça nous fait triper. Ne pas hésiter non plus à jouer la carte de l’humour, en disant que l’on est conscient du fait que la feature que l’on montre est une torture pour un non-technique, et qu’on n’a aucune pitié.

Une itération complètement dédiée à une migration d’hébergeur ? Je ne vois pas ce qu’il y a de plus chiant pour un fonctionnel. Confronté au cas, j’ai botté en touche en faisant une présentation avec slides, montrant les enjeux, le besoin de migrer, le planning, pourquoi ça nous prend du temps, etc. Ce n’est pas du tout ce que devrait être une démo, mais pour ce coup là, j’ai trouvé ça plus judicieux à ce moment là que de montrer à quel point nos cookbooks chef s’exécutent bien.

##Et tout ça c’est facile ?

Putain non.
