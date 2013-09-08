---
layout: post
title: PirateBox sur laptop
categories:
- Coding
- DIY
- Tutoriel
type: post
---
![](/assets/2011/11/piratebox-logo.png)

Cela fait quelque temps que je me renseigne sur le principe de la Piratebox, vous pouvez en faire de même <a title="wiki_piratebox" href="http://wiki.daviddarts.com/PirateBox" target="_blank">là</a>( la version 0.3-3 V1.2). Puisque je ne parlerai ici que de l'aspect technique de l'installation sur un ordinateur portable.

J'ai suivi ce tuto en pensant que tout se passerait bien mais j'ai eu plusieurs erreurs en voulant lancer le init.d/piratebox start.  Je vais donc détailler ici les modifications que j'ai effectué et quels fichiers modifier pour customiser un peu votre piratebox.

Premièrement:

→ Fichier `bin/piratebox_setup_wlan.sh`

Un seul = est nécessaire pour une comparaison entre une variable et une chaîne.

La ligne 51 devient:

{% highlight bash %}
if [ $2 = "start" ] ; then
{% endhighlight %}

La ligne 68 devient:

{% highlight bash %}
elif [ $2 = "stop" ] ; then
{% endhighlight %}

→Fichier `conf/hosts`

Pour régler les problèmes de redirection vers piratebox.lan, sur la page d'accueil en local ( sur 192.168.77.1) le iframe contenant le chat pointe vers piratebox.lan:8002 et non plus 192.168.77.1:8002. J'ai donc rajouter quelques ligne au fichier conf/hosts ( que j'ai ensuite copier dans mon fichier /etc/hosts pour accéder en local à piratebox.lan comme précisé sur le tutoriel).

{% highlight bash %}
192.168.77.1  piratebox
192.168.77.1  pirate.box
192.168.77.1  piratebox.lan
{% endhighlight %}



J'avoue que je sais plus trop bien pourquoi j'ai rajouter le pirate.box, je devais avoir une bonne raison.

Avec ces modifications de faites votre piratebox devrait marcher, mais si vous voulez aller plus loin:

Pour les redirections du port 80:

→Fichier `init.d/piratebox`

Rajouter ligne 106

{% highlight bash %}
#Redirection with iptabes, uncomment if you got some trouble with that
#redir.sh $INTERFACE $IP :80
{% endhighlight %}

Et donc le fichier redir.sh à créer dans bin/

→Fichier bin/redir.sh

{% highlight bash %}
#!/bin/bash
#script to redirect all connection via port 80 to specified IP
#example of parameter:
#redir.sh wlan0 192.162.77.1:80
if [ $# -eq 3 ] &amp;&amp; [ -n $1 ] &amp;&amp; [ -n $2 ] ; then
echo "setting up iptable"
iptables -t nat -A PREROUTING -i $1 --protocol tcp --match tcp --destination-port 80 -j DNAT --to-destination $2$3
else
echo "redir.sh <interface> <ip:port>"
fi
{% endhighlight %}

Pour la personnalisation le principal fichier à modifier est conf/piratebox.conf et en particulier les variables TEXT et CHATMSG.

Vous pouvez par exemple faire une traduction comme ceci:

→Fichier conf/piratebox.conf

À partir de la ligne 68

{% highlight html %}
#Text on droopy
# old TEXT="<p><br><b>1.</b> Learn more about the project <a href="http://$HOST:8001/.READ.ME.htm"><b>here</b></a>.<p>
<b>2.</b> Click above to begin sharing.</p><b>3.</b> Browse and download files <a href="http://$HOST:8001"><b>here</b></a>."
TEXT"<b>1.</b> En apprendre plus à propos du projet <a href="http://$HOST:8001/readme.html" target="_parent"><b>ici</b></a>.
<p><b>2.</b> Cliquez sur le bouton ci dessous pour commencer à partager</p>
<b>3.</b> Naviguer et télécharger des fichiers <a href="http://$HOST:8001" target="_parent"><b>ici</b></a>.<br>"
TEXT2="<b>1.</b> Learn more about the project <a href="http://$HOST:8001/readme.html" target="_parent"><b>here</b></a>.
<p><b>2.</b> Click button below to begin sharing.</p>
<b>3.</b> Browse and download files <a href="http://$HOST:8001" target="_parent"><b>here</b></a>.<br>"

#Configuration for chat  (If you decide to move the chat folder, you have to change /opt/piratebox/chat/cgi-bin/py* files )
CHATFOLDER="/opt/piratebox/chat"
#Inititiation Chat-Message
CHATMSG="<date>00:00:00</date>&amp;nbsp;&amp;nbsp;<name>PirateBox:</name>&amp;nbsp;&amp;nbsp;&amp;nbsp;<data class='def'>Parlez et partagez des fichiers anonymement !</data><br>"
CHATMSG2="<date>00:00:00</date>&amp;nbsp;&amp;nbsp;<name>PirateBox:</name>&amp;nbsp;&amp;nbsp;&amp;nbsp;<data class='def'>Chat and share files anonymously!</data><br>"
{% endhighlight %}

Et sans oublier le fichier readme.html à placer dans share/ que vous pouvez personnaliser comme vous le souhaiter, les images seraient à placer dans src/ ( aucun lien vers du contenu 'internet').

→Fichier share/readme.html ( à créer)

{% highlight html %}
<h2>Description</h2>

<p>PirateBox is a self-contained mobile collaboration and file sharing device. Simply turn it on to transform any space into a free and open file sharing network.</p>

<h2>Mision</h2>

<p>Share Freely! Inspired by pirate radio and the free culture movements, PirateBox utilizes Free, Libre and Open Source software (FLOSS) to create mobile wireless
file sharing networks where users can anonymously share images, video, audio, documents, and other digital content.</p>
{% endhighlight %}

Je pense avoir fait le tour de la question, personnellement j'ai installé une piratebox sur mon laptop en attendant dans installer une sur un routeur sans-fil, ce qui sera bien plus pratique. Si vous avez des questions, des remarques, une erreurs dans ce que j'ai écrit, n'hésitez pas: commentaire ou formulaire de contact.

Bien sur cet article n'incite en rien au téléchargement illégal ni à la copie de contenu copyrighté, mais au partage. À bon entendeur. ;)
