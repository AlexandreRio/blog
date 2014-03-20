---
layout: post
title: Docker sur Kimsufi OVH
---

Si vous souhaitez installer [Docker](https://docker.io) sur un serveur OVH il vous faudra de la patience et beaucoup de requêtes à un moteur de recherche pour comprendre les erreurs.

Voilà rapidement ce qu'il faut faire pour y parvenir :

* compiler un kernel soi-même, de version 3.8 minimum comme recommandé par la doc mais ceux fournis par OVH ne supportent un certain nombre de fonctionnalités nécessaires au fonctionnement de LXC. Cet article explique très bien la marche à suivre: [http://blog.blaisethirard.com]( http://blog.blaisethirard.com/creer-des-serveurs-virtuels-debian-7-wheezy-avec-lxc-sur-un-dedie-ovh-kimsufi-2/)
* En passant par les dépôts Ubuntu il est possible d'obtenir un paquet compatible avec Debian 7, là c'est la [doc](http://docs.docker.io/en/latest/installation/ubuntulinux/) officielle qu'il faut suivre
* Contrairement à ce que j'ai pu trouver sur pas mal d'articles il ne faut la ligne
`none /sys/fs/cgroup cgroup defaults 0 0` dans `/etc/fstab`
* modifier le service docker (/etc/init.d/docker) en le remplaçant par celui indiqué sur cette [issue](https://github.com/dotcloud/docker/issues/4568#issuecomment-37270398)
* plus un détail mais il peut être utile de modifier le répertoire où sont stockés les conteneurs, par défaut à la racine.
Pour ce faire ajoutez à votre `/etc/default/docker` la variable `DOCKER_OPTS="-g /path/des/datas"`

Et voilà c'est à peu près tout, en suivant ces quelques points vous devriez pouvoir faire tourner Docker.

Je tiens à remercier [Fred](http://fspot.org/) pour m'avoir pointé du doigt le problème des noyaux OVH et fourni le lien pour la compilation du noyau.
