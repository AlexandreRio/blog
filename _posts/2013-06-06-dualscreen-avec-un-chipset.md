---
layout: post
title: Dualscreen avec un chipset
categories:
- Astuce
- Coding
status: publish
type: post
published: true
---

Lorsque l'on a un ordinateur avec un chipset ( une carte graphique intégrée à la carte mère ) il est pas toujours évident de bien gérer son dualscreen, il faut faire avec les outils fournis avec sa distro et ils sont souvent bien moins efficace que ceux fournis avec les drivers graphique des cartes NVidia et autres.

![Gnome display interface](/assets/2013/06/gnome_display.png)
Celui-ci ne permet pas d'ajuster les positions relatives des écrans.

J'ai donc écrit un petit script qui se base sur xrandr pour pouvoir gérer différents types de dualscreen :

 * Les deux écrans sont à l'horizontale côte à côte,</li>
 * les deux écrans sont à l'horizontale côte à côte et un des deux est en orientation verticale, pratique pour les développeurs,</li>
 * ou encore si les deux écrans sont à l'horizontale l'un au dessus de l'autre</li>

Pour l'utiliser il suffit de faire :
{% highlight bash %}
./display.sh
./display.sh - -vertical
./display.sh - -above
{% endhighlight %}

{% gist 5720045 %}

Dans certains cas il arrive que tint2, l'utilitaire de barre de tâches, plante et affiche un écran noir au survol de la barre avec la souris, c'est pourquoi il faut le relancer, pensez à adapter le chemin vers votre fichier de configuration si vous utilisez tint2, sinon supprimez les 2 dernières lignes.

![Tint2 bug](/assets/2013/06/Screenshot-05232013-053142-PM-624x350.png)
Quand on touche à l'affichage sans relancer tint2

Et voilà, ce sera tout, à une prochaine fois ! :-)
