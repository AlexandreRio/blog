---
layout: post
title: My Data back !
categories:
- Internet
---

Suite à la lecture du rédacteur en chef de rue89.fr «[Ma semaine sans google](http://www.rue89.com/2013/10/11/semaine-sans-google-13-mail-sans-gmail-ca-paye-246434)» je me suis d'abord dit :

    «C'est bien qu'une personne qui ne soit pas «du secteur IT» (enfin vous me comprenez, geek toussa ) prenne des décissions comme ça et communique dessus.»

Outre le fait que l'initiative soit dès le début prévue comme temporaire je me suis ensuite remis en question. Même si j'utilise beaucoup d'outils qui me permettent d'avoir plus d'emprise sur mes données c'est encore très loin d'être parfait.

L'article de rue89 m'a donc donné la motivation qu'il me fallait pour avoir encore un plus de données «chez moi».

Voilà ce que j'ai changé

##Mozilla-sync

J'utilise exclusivement pour la navigation et le service Mozilla Sync pour mémoriser et synchroniser mes mots de passe et bookmarks. J'ai donc installé mon propre serveur Sync plutôt que d'utiliser ceux de Mozilla, même si les données sont chiffrées et théoriquement illisibles par une tierce personne sans la clé de récupération.

##Carddav

La chose qui me gênait le plus était d'utiliser Google pour synchroniser mes contacts entre mon téléphone sous Android et mon laptop, je faisais des exports en csv que j'importais dans Thunderbird.

Conséquence : installation d'un serveur carddav pour tout synchroniser ça.
Sur Android j'utilise [DAVDroid](http://davdroid.bitfire.at/what-is-davdroid), sur mon laptop j'utilise [pycarddav](https://github.com/geier/pycarddav/), qui s'utilise en CLI donc très pratique pour Mutt ( mais pas que).

##Caldav

Pour synchroniser ses agendas, il faut juste avoir un Adapter caldav pour que l'agenda d'Android puisse se synchroniser.

##Cyanogen mod ( cf conf sur les baseband )


