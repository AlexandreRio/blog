---
layout: post
title: Un peu d'humour de geek?
categories:
- Coding
- Humour
type: post
---
Bien le bonjour!

Aujourd'hui je vous propose un Shellscript Bash pour afficher des blagues de geek. o/

En fait ceux sont les mêmes blagues qui s'affichent en haut à droite de ce blog ( d'ailleurs certaines ont encore des problèmes d'encodage mais j'y travaille).

Pour exécuter ce code il faut la librairie zenity, installée par défaut sous Ubuntu, qui permet d'afficher des boites de dialogue GTK+,  s'il n'est pas présent sur votre machine un `sudo apt-get install zenity` devrait suffire.

Le script est donc disponible <a href="http://orbital-project.kegtux.org/programmes/bdg.sh">ici</a> ou via la commande:

`cd $HOME/Bureau &amp;&amp; wget http://orbital-project.kegtux.org/programmes/bdg.sh &amp;&amp; chmod +x bdg.sh &amp;&amp; ./bdg.sh`



Et pour ceux qui ont la flemme de le télécharger voilà le code source:

{% highlight bash %}
#!/bin/bash
#                               Script d'affichage de blague de geek
#                                   Necessite le paquet zenity
#################################################################################################
#                           Par Orbital: http://orbital-project.kegtux.org/blog/
#                               http://twitter.com/Rio_Alexandre
#################################################################################################

Cache="$HOME/.bdg_cache"
let "continuer=1"
if [ ! -d $Cache ]
then
 mkdir $Cache
fi
chmod 777 $Cache
cd $Cache
while [ $continuer -eq 1 ]
do
 rm *.php
 wget http://orbital-project.kegtux.org/programmes/list.php

 zenity --info --text="`cat list.php`" --title="Blague de geek" --width=200 --height=150
 zenity --question --ok-label="une autre!" --cancel-label="Quitter" --text="Continuer ?"
 if [ $? -eq 0 ]
 then
 let "continuer = 1"
 else
 let "continuer = 0"
 fi

done
{% endhighlight %}

Le script créera le dossier .bdg_cache pour stocker la blague à afficher, le dossier est caché et est vidé à chaque exécution donc il devrait pas trop gêner.

Et voilà le rendu:

![](http://orbital-project.kegtux.org/blog/wp-content/uploads/2011/05/script_bdg.png)

Quand j'aurais le temps je verrai pour rajouter des couleurs au titre, à l'auteur et à la date.

En espérant qu'elles vous feront rire. ++
