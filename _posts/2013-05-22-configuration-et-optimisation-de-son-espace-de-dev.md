---
layout: post
title: Configuration et optimisation de son espace de dév'
categories:
- Astuce
- Coding
- Tutoriel
status: publish
---
#Configuration et optimisation de son espace de dév'
Quand je bosse dans un lieu public on me demande souvent ce que j'utilise comme distribution, comme Desktop Environment ou encore comme éditeur de texte / IDE.
Parce que oui ça ressemble pas à la dernière version d'Ubuntu avec Gnome Unity, pour la simple et bonne raison que je les trouve peu ergonomique et peu configurable.

J'ai longtemps utilisé un laptop avec un écran de 15,4" suffisamment grand pour être confortable mais pas trop pour rester facilement transportable, j'ai toujours eu du mal avec les laptops 17"…
Depuis quelques mois je suis passé à un EliteBook 2570p, vraiment parfait pour coder en déplacement : très léger, très compact, autonomie de 3 à 4 heures avec la batterie «double». Je ne vais pas faire une critique de l'ordinateur portable, juste qu'avec un écran de 12,5" les barres d'états / de menus / d'outils occupent très vite une part importante de l'écran.
##Environnement de bureau
J'ai longtemps utilisé Gnome 2 puis quand est sortit Gnome 3 «Gnome Shell» je suis passé à [OpenBox](http://openbox.org/) avec un thème Darksun et tint2 pour la barre de taches. J'utilise [Conky](http://conky.sourceforge.net/) pour le monitoring. J'ai flouté un flux RSS.
Au passage, si vous avez un problème de transparence sur les icônes de taches de [Tint2](http://code.google.com/p/tint2/) regardez du côté des paramètres de Compositor ou du Compositing.

![Desktop Screenshot](http://alexrio.fr/blog/wp-content/uploads/2013/05/desktop.png)

##Optimisation
Après avoir optimisé l'espace de travail il reste à optimiser les outils de développement. De manière générale l'objectif est de pouvoir tout contrôler depuis le clavier, devoir lâcher le clavier pour prendre la souris faisant perdre du temps.

Pour optimiser la frappe je suis passé à la disposition [Bépo](http://bepo.fr/wiki/Accueil) depuis maintenant presque un an.

###Le terminal
Pour développer je fais presque tout avec [Vim](http://www.vim.org/), avec les plugins:
* [Vim_getset](http://www.vim.org/scripts/script.php?script_id=490) : ajout de getter / setter pour les attributs d'une classe Java
* [Vim_nerdtree](http://www.vim.org/scripts/script.php?script_id=1658) : pour faciliter la navigation dans les dossiers depuis Vim
* [Vim_tabular](https://github.com/godlygeek/tabular) : pour des lignes en fonctions d'un pattern, le = par exemple
* [Vim_vaxe](https://github.com/jdonaldson/vaxe) : pour le support du langage Haxe
* [Vim_powerline](https://github.com/Lokaltog/powerline) : pour faciliter la gestion des buffers
* [Eclim](http://eclim.org/) : pour intégrer les fonctions d'eclipse à vim, je commence juste à m'en servir
* et bien sur [Vim_pathogen](https://github.com/tpope/vim-pathogen) pour gérer l'installation des plugins

![Vim](http://alexrio.fr/blog/wp-content/uploads/2013/05/vim.png)

Au lieu de devoir lancer plusieurs terminaux j'utilise le multiplexer [tmux](http://tmux.sourceforge.net/).
Dans la status bar de tmux l'état de mes boites mails et une horloge, comme ça même en fullscreen tout est disponible.
![tmux](http://alexrio.fr/blog/wp-content/uploads/2013/05/tmux.png)
J'utilise 2 sessions avec tmux, la première est celle qui apparait à l'ouverture du terminal, elle est vide. La seconde contient 3 onglets avec une instance de mutt dans chaque.

Les emails sont récupérés en IMAP avec [offlineimap](http://offlineimap.org/), les mots de passe sont stockés par gnome-keyring, allez voir l'article de [Gnome_keyring](http://jason.the-graham.com/2011/01/16/gnome_keyring_with_msmtp_imapfilter_offlineimap/) si vous voulez automatiser dans une cron.

J'utilise aussi le client [TTYtter](http://www.floodgap.com/software/ttytter/"> ( j'y reviendrai plus tard ).

###Le navigateur
J'utilise Firefox, sur le canal stable, je suis pas développeur donc pas besoin du support des dernières fonctions avant qu'elles sortent.

![Firefox](http://alexrio.fr/blog/wp-content/uploads/2013/05/firefox.png)

Le plugin le plus important que j'utilise est clairement Pentadactyl, il permet d'utiliser Firefox avec les mêmes raccourcis claviers que Vim, puisque tout se fait au clavier tous les menus et barres peuvent être désactivés pour gagner encore plus d'espace.
J'ai modifié le hint-mode, qui permet de «cliquer» sur les liens d'une page à l'aide du clavier, pour le rendre plus ergonomique. Les lettres proposées correspondent à la partie gauche d'un clavier bépo, le hint-mode se déclenchant avec la touche f, située à droite du clavier. Le style css des propositions correspond peu ou prou à celui du plugin chrome Vimium qu'un ami utilisait et qui est bien plus lisible.

J'ai rebindé quelque commande, soit pour s'adapter à un mapping bépo soit pour gagner du temps, pour la commande :downloads par exemple.

Un des points fort de pentadactyl est de pouvoir lancer des commandes du système, ça ne remplace pas du tout un shell mais peut s'avérer utile dans certains cas, comme par exemple appeler le client ttytter, on peut imaginer le cas suivant :
Touche . pour passer en mode commande, et la commande :twitter Hello world !
Pouvoir tweeter en si peu de keystroke et sans changer de page ça c'est de l'optimisation !

##Ce qu'il me reste à faire / améliorer

<blockquote class="twitter-tweet" lang="xx-lc">Aujourd'hui je passe à offlineIMAP et mutt pour lire mes mails o/ <a href="https://twitter.com/search/%23FullCLI">#FullCLI</a> – Alexandre Rio (@Rio_Alexandre) <a href="https://twitter.com/Rio_Alexandre/status/335373857349308418">May 17, 2013</a></blockquote>

<blockquote class="twitter-tweet" lang="xx-lc">Oui parce que parfois <a href="https://twitter.com/search/%23Thunderbird">#Thunderbird</a> me bouffe 100% d'un core, met 10min a récupérer un mail de 2 lignes de texte. <a href="https://twitter.com/search/%23TweetPrécédent">#TweetPrécédent</a> — Alexandre Rio (@Rio_Alexandre) <a href="https://twitter.com/Rio_Alexandre/status/335374647610732544">May 17, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Ça fait peu de temps que j'essaie de remplacer Thunderbird, il me reste encore à configurer mes filtres et la partie SMTP.

Ça fait pas mal de temps que j'utilise Conky mais je trouve que j'en ai de moins en moins l'utilité, à l'avenir je pense le simplifier drastiquement pour avoir un bureau plus épuré, et puis niveau couleur c'est pas trop ça…

##Conclusion
Bien que certains aspects soient un peu «gadget» ma conf' me permet de gagner un temps considérable par rapport à une distrib' «classique».
N'hésitez pas à laisser un commentaire pour me faire part de vos remarques, questions ou suggestions ou si vous voulez que je rajoute un fichier de conf, j'ai inséré les plus importants et les plus modifiés.

###Les articles dont je me suis très largement inspiré
* [Paul Rouget](http://paulrouget.com/e/myconf/) pour son thème vim et thème de bureau ainsi que pour l'idée de faire ce genre d'article.

* [Jason's Blog](http://jason.the-graham.com/2011/01/10/email_with_mutt_offlineimap_imapfilter_msmtp_archivemail/) pour la partie gestion des emails.
