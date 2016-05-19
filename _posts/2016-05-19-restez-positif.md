---
layout: post
title: Oui, tout est cassé
---

Cette article est une réponse à ce tweet :

<blockquote class="twitter-tweet"><p lang="fr" dir="ltr">les gens qui sont positifs envers la technologie et qui /bossent dans l&#39;info/, c&#39;est quoi votre truc?</p>&mdash; wxcafé(8) (@Wxcafe) <a href="https://twitter.com/Wxcafe/status/732852009355882497">May 18, 2016</a></blockquote>

Je vais essayer de reprendre quelques arguments exprimés et donner mon avis.

    Everything is broken

Oui, tout logiciel a des failles, tout hardware a des failles. Aucun système n'est sûr. Chaque brique a des failles, chaque système complexe n'est pas amoncellement de failles.
Ma réponse serait tout simplement de ne pas dépendre de ces systèmes, de considérer que tout ce qui est sur les Internets est accessible.
En bloquant, refusant, limitant tout ce qui est trop compliqué ou trop obscur (dans le sens ou l'opérateur d'un service refuse exprès de donner des informations sur le fonctionnement de son service), on se rend compte qu'au final très de choses sont vraiment utiles et nécessaires.

Je trouvais mon téléphone «trop» compliqué : ROM cyanogen, plus de surcouche opérateur, plus de Google Services. Un gestionnaire d'application, F-Droid, contenant uniquement des applications dont le code source est accessible. Résultat, les applications sont en moyenne (donnée très scientifiquement calculée par mon impression quand j'installe des appli) bien plus légères et demandent très peu de privilège par rapport au système.
C'est très loin d'être parfait mais c'est déjà bien mieux. Pratiquement aucune application n'accède à Internet ni n'accède à plus de données que nécessaire, pas d'accès aux régies de pub.

Si personne n'agrège de données ça laisse moins de raison de vouloir pénétrer un système, puisque après tout, tout système est faillible.

Si plus un système devient gros plus il contient de faille et de bug alors autant privilégier les systèmes simples.
C'est un principe de base de la programmation, Keep It Simple Stupid (KISS) ou même la phisolophie UNIX, qui ne doit pas uniquement se cantonner à la programmation.

Je passe énormément de temps sur mon ordinateur, comme beaucoup de gens je veux que «ça marche, tout simplement». La solution de beaucoup de monde (je ne juge pas, ça a ses avantages) est d'installé le système que tout le monde utilise, plus facile de trouver une solution si ça pète.
Ma solution est plutôt de n'installer que ce dont j'ai besoin, un système minimal sera bien moins enclin à planter.

    Programming sucks

Oui et non, je travaille principalement sur des compilateurs et mon domaine de recherche inclut les Domain Specific Languages alors mon avis doit être biaisé. Si on regarde la masse des développeurs au fil des années et l'évolution des langages de programmation on comprend que c'est un passage obligatoire.

Gérer soi même les registres c'est chiant ? Le compilateur s'en charge. Gérer manuellement la mémoire dynamique c'est chiant ? Le compilateur/runtime s'en charge. Le typage c'est chiant ? Le compilateur/runtime s'en charge.

Il y aura toujours des aspects de la programmation qui seront chiant, à force les gens feront des bibliothèques/frameworks/whatever pour le faciliter, à force ça fera partie intégrante d'un nouveau langage et le cercle reprendra.

Il y avait surement d'autres arguments exprimés dans les articles mais je voulais au moins exprimer mon point de vue sur ces points.
