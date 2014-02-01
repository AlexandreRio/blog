---
layout: post
title: SuchSeriesCrawling
categories:
- Internet
- Coding
---

J'en ai déjà un peu parlé sur Twitter, j'ai commencé un petit projet de «crawler».

L'objectif du programme est de pouvoir visualiser et comparer les moments de sorties des épisodes de séries TV sur différents trackers.

Dans l'idéal sous la forme d'un graphe on montrant la propagation d'une sortie par exemple en se basant sur la team qui la faite.

Dans la technique ça donne un programme qui se connecte sur différents sites de tracker, un maximum, et log le flux RSS. Pour chaque entrée du flux on parse les informations dont on a besoin et les stocke dans une base de données pour pouvoir les exploiter plus tard.

Voilà, rien de bien compliqué ; pour le moment le programme récupère bien les sorties et je suis en train d'écrire l'ajout à la base de données. Je pense faire une version 1.0 quand l'ajout sera fini et qu'il pourra produire une bdd «propre» et réutilisable, la partie graphique viendra après.

Les sources sont sur [github](https://github.com/AlexandreRio/SuchSeriesCrawling), il manque la liste des trackers, je vous laisse le soin d'utiliser la votre.
