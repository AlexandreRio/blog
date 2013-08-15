---
layout: post
title: La TV dans VLC pour les abonnés Orange.
categories:
- Astuce
- Coding
type: post
---
Mise à jour du 01/10/11:
#Il semblerait que cette méthode ne fonctionne plus, Orange a changé sa façon de diffuser sa TV en ligne.

<hr />

Un p'tit script en bash pour regarder la télé dans vlc ou l'enregistrer. Pour changer de chaîne il faut relancer le script, si vous avez déjà essayé ADSLTV ou que vous utilisez le site de orange.com ( et son lecteur tout pourri ) pour regarder la télé vous savez déjà que toutes les chaînes de sont pas présentes ( il manque entre autre TF1, M6 et W9). Bon je crois que j'ai fait le tour, j'ai aucun bug à signaler mais si vous voyez un truc à améliorer/corriger comme d'hab' commentaire ou mail dans la partie "contact".

{% highlight bash %}
#!/bin/bash
#                           Script de récupération de flux vidéo TV ADSL
#                         Ne fonctionne que pour les abonnés au FAI Orange
#                                          Nécessite vlc
#################################################################################################
#                           Par Orbital: http://orbital-project.kegtux.org/blog/
#                                        http://twitter.com/Rio_Alexandre
#################################################################################################
cd ~/scripts/orange #Chemin à adapter
if [ $# = 4 ]
then
c=$1
action=$2
fichier=$3
duree=$4
else
c=$(zenity --list --title="Choisir la chaîne" --hide-column=1  --column="id" --column="Chaîne" 26 "Nolife" 5 "France 2" 6 "France 3 Nat" 7 "France 5" 8 "Arte" 9 "Direct 8" 10 "NT1" 11 "NRJ12" 12 "LCP/PS" 13 "France 4" 14 "BFM TV" 15 "I&gt; Télé" 43 "Direct Star" 16 "France Ô" 17 "Video à la demande" 18 "Orange sport Info" 19 "Orange Sport" 20 "AB Moteurs" 21 "OCS à la demande" 22 "Orange Ciné Max" 39 "Orange Ciné Happy" 40 "Orange Ciné Choc" 41 "Orange Ciné Novo" 42 "Orange Ciné Géants" 23 "TV5 Monde" 24 "Liberty TV" 25 "Fashion TV" 26 "No life" 27 "Trace TV" 28 "France 24 (en français)" 29 "BBC World" 44 "CNN International" 30 "France 24 (en anglais)" 31 "France 24 (en arabe)" 32 "Al Jazeera" 33 "Guysen TV" 34 "Demain TV" 35 "Poker Channel" 36 "TV8 Montblanc" 37 "CCTV F" 38 "Chanel one Russia") || exit

action=$(zenity --list --title="Choisir l'action" --hide-column=1  --column="id" --column="Action" 1 "Visualiser" 2 "Enregistrer") || exit
if [ $action = 2 ]
then
fichier=$(zenity --title="Nom du fichier" --entry --text "Entrer le nom du fichier précédé du chemin") || exit
duree=$(zenity --title="Durée enregistrement" --entry --text "Entrer la durée de l'enregistrement en minutes") || exit
fi
fi
if [ $action = 1 ]
then
wget -qO- 'http://chaines-tv.orange.fr/pfs-webapp/user/live/channel/'$c'/url.json?resolution=MEDIUM&amp;subtitle=false' | grep -o 'http[^"]*' | sed 's,http://,mmsh://CDLYOS02.se.,' &gt; link.m3u
vlc link.m3u
else
mplayer -dumpstream -dumpfile  $fichier".wmv" $(wget -qO- 'http://chaines-tv.orange.fr/pfs-webapp/user/live/channel/'$c'/url.json?resolution=MEDIUM&amp;subtitle=false' | grep -o 'http[^"]*' | sed 's,http://,mmsh://CDLYOS02.se.,') &amp;
pid=$!
let duree=$duree*60
sleep $duree
kill $pid
fi
{% endhighlight %}

Au passage je vous conseille la chaîne Nolife, ce n'est pas pour rien que je l'ai rajoutée au début de la liste.;)
