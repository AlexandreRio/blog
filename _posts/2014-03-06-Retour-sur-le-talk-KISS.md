---
layout: post
title: Retour sur le talk «KISS» à la Cantine Numérique
---

Le 12 février dernier s'est tenu à la cantine numérique de Rennes un talk nommé «Pourquoi faire simple quand on peut faire
compliqué ?» présenté par Frédéric Bouchery et qui tentait de répondre à la problématique

    «Pourquoi, inévitablement, tous les projets informatiques tendent à se complexifier ?
    Peut-on vraiment appliquer le principe "KISS" (Keep It Simple Stupid) ?»

Je ne vais pas résumer l'intégralité de sa présentation mais plutôt reprendre certains points abordés et les détailler un peu.

## Complexité
Tout projet tend à se complexifier avec le temps, un premier abordé à été de déterminer d'où vient cette complexité

## L'importance de l'expérience dans le choix des outils

Avant de commencer à coder on analyse les besoins, puis on détermine les technologies qui seront à utiliser.
Là on peut arriver au cas de figure suivant : l'architecte maitrise ou affectionne un langage, disons PHP, alors que son équipe a plus d'expérience par exemple en JEE.

### Avoir une mauvaise expérience sur un framework

On a tous connu des frameworks qui ont l'air super bien «sur le papier», seulement nos besoins sont rarement aussi simples que les quelques cas d'utilisations documentés sur le site, de même le super framework du dernier n'est pas forcément approprié pour ce projet ci, les projets ne sont pas toujours les mêmes.
Parfois la raison est simplement que le framework était trop jeune la première fois qu'on l'a utilisé et cette mauvaise expérience nous a marqué.

Tout cela peut être accentué par le [*Syndrome du Not Invented Here*](https://fr.wikipedia.org/wiki/Not_Invented_Here).

_Il faut adapter les besoins aux outils et non l'inverse._

## Le problème des développeurs expérimentés

À ces problèmes d'architectures viennent s'ajouter des problèmes de développement.

Tout d'abord le manque de développeur expérimenté, qui s'explique du fait que lorsqu'un développeur arrive à un certain niveau d'ancienneté les entreprises préfèrent lui donner plus de responsabilité voire le faire passer chef de projet.
Il en ressort un manque d'expert d'une technologie donnée.

## Quelques conseils

Tout d'abord les bonnes pratiques ne sont pas des lois, il ne faut pas hésiter à les enfreindre ou les modifier en fonction du projet et des développeurs.

Il faut se méfier de ce que l'on peut lire sur certains outils, il vaut mieux se fier à l'expérience de ses développeurs mais ne pas hésiter à faire des paris.

Un bon moyen de prendre une décision lors du choix d'un outil est la *matrice de décision* qui consiste à affecter un coefficient à différents critères comme :

- Le niveau de maitrise de l'outil par l'équipe de développement
- Le coût de la licence
- La facilité de mise en place de la fonctionnalité 1, 2, N

Bien sur les valeurs à associer sont totalement subjectives.

### Pour le code

De manière générale, surveiller le code et pas uniquement avec des outils qui feront des statistiques que personne ne regardera.

Concevoir et développer en binôme, idéalement un moins expérimenté avec un plus expérimenté.

Former et entraîner ses développeurs autant que possible

## Pour aller plus loin

* [Les slides présentés au forum php 2013](http://forumphp2013-bouchery.rhcloud.com/#/)
* [L'événement meetup](http://www.meetup.com/DevCamp/events/163730602/)
* [Le site de la Cantine Numérique Rennaise](http://www.lacantine-rennes.net/)
