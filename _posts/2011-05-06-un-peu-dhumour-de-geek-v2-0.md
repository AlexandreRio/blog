---
layout: post
title: Un peu d'humour de geek? V2.0
categories:
- Coding
- Humour
type: post
---
Bonjour!

Comme je suis en vacance j'ai eu le temps de revoir mon <a href="http://orbital-project.kegtux.org/blog/2011/05/01/un-peu-dhumour-de-geek/">script de blagues de geek</a>! Le  code est donc bien plus propre et léger, de plus l'affichage a même été refait!

Voilà le code source:

{% highlight bash %}
#!/bin/bash
#                           Script d'affichage de blague de geek V2.0
#                                   Necessite le paquet zenity
#################################################################################################
#                           Par Orbital: http://orbital-project.kegtux.org/blog/
#                               http://twitter.com/Rio_Alexandre
#################################################################################################

let "continuer=1"

while [ $continuer -eq 1 ]
do
 message=`wget -O  - http://orbital-project.kegtux.org/programmes/bdg_script.php`

 zenity --info --text="$message" --title="Blague de geek"
 zenity --question --ok-label="une autre!" --cancel-label="Quitter" --text="Continuer ?"
 if [ $? -eq 0 ]
 then
 let "continuer = 1"
 else
 let "continuer = 0"
 fi

done
{% endhighlight %}

Et le nouveau design:

![](/assets/2011/05/bdg_scrip_v2.png)

L'encodage merdouille encore un petit peu, quand c'est le cas ou rien de n'affiche et le script vous demande si vous voulez continuer, ou on vous dit que "Toutes les mises à jour sont complètes." ( pour des raisons qui me sont inconnues...)

À la prochaine!
