---
layout: post
title: S-Paste un pastebin minimaliste
categories:
- Coding
- Internet
---
Bonjour à tous et toutes !

Vous connaissez surement le principe des pastebin, vous uploadez le contenu d'un fichier sur un serveur, il génère un lien unique pour que vous puissiez le partager.

Seulement beaucoup d'aspects peuvent être gênants:

* Malgré les "programmes tiers" il est pas toujours intuitif ni rapide d'uploader un fichier
* Puisque les sites sont publics et très sollicités, les liens générés doivent être longs pour rester uniques
* Même si ce que l'on poste est généralement public on a pas forcement envie de se faire indexer par les robots
* On peut pas être sur de l'utilisation qui est faite des données (code proprio)
* Surement encore plein d'autres raisons auxquelles j'ai pas pensé…

C'est donc dans cette optique que j'ai écrit 'Simple Paste' ( abrégé s-paste ). Un script en ligne de commande côté client qu'on appelle en spécifiant le fichier souhaité, côté serveur ça se contente de créer un fichier avec le contenu envoyé

Puisque ça tourne sur son serveur perso pas besoin de générer des noms de fichier très long, je suis parti sur 5 caractères avec alphabet minuscule et chiffres (36^5 = 60 466 176 fichiers théoriques) mais 4 pourraient très bien faire l'affaire.

Voilà le code du client :

##/!\ Le code n'est pas du tout à jour, visitez le github ! /!\

###[https://github.com/AlexandreRio/s-paste](https://github.com/AlexandreRio/s-paste)

{% highlight bash %}
#!/bin/bash
#
# Minimalistic pastebin tool, uploads file and return a link.
# The server part can be found here:
# https://github.com/AlexandreRio/s-paste
#
# /!\ Don't forget to edit the url /!\
#############################################################
#         By Alexandre Rio / Orbital
# http://alexrio.fr/    https://twitter.com/Rio_Alexandre
#############################################################
#
#    See LICENSE file for copyright and license details
#
#############################################################

help="Usage: \n- ./spaste [you can write an URL here]\n- ./spaste -f
file/path/here"
url="alexrio.fr/p/"

if [ $# -eq 2 ] &amp;&amp; [ $1 = '-f' ]
then
    curl -d "data=`cat $2`" $url
elif [ $# -eq 1 ] &amp;&amp; [ $1 = '--help' ]
then
    echo -e $help
elif [ $# -eq 1 ]
then
    curl -d "data=$1" $url
else
    echo -e $help
fi
{% endhighlight %}

Et le code serveur :

{% highlight php %}
<?php
if(!empty($_POST))
{
  $url = 'http://alexrio.fr/p/'; // Your server location
  $size = 5; // Lenqht of the name of the file
  do {
    $chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
    for($i=0; $i<$size; $i++)
    {
      $fileName .= $chars[rand()%strlen($chars)];
    }
  }
  while(file_exists($fileName));

  $file = fopen($fileName,'a+'); // Don't forget to check the permission
  fputs($file,$_POST["data"]);
  fclose($file);

  $number = sizeof(glob("*")) - 1; // Count the number of file less the php file.
  print "Number of files: $number\nYour link:\n$url$fileName\n";
}
else {
  print 'This page only accept POST method.';
}
?>
{% endhighlight %}

Pour vous tenir informé du projet ou pour contribuer ( surtout pour la sécurité ) et pour récupérer les sources plus facilement je vous invite à faire un tour sur le <a href="https://github.com/AlexandreRio/s-paste">github</a>.
