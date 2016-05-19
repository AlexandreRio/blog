---
layout: post
title: Configurer Samba pour une machine virtuelle.
categories:
- Astuce
- Tutoriel
type: post
---
# Introduction:

Ayant passé un long ( trop long ?) moment sous windows avant de migrer à linux, j'ai gardé mais petites habitudes avec certains logiciels qui ne tournent que sous windows. Principalement le logiciel Zune, qui me permet de rajouter de la musique sur ce dernier. J'ai très vite utilisé une machine virtuelle pour avoir Zune, mais comment faire pour accéder à mes musiques/vidéos/images depuis cette machine ? Même si le logiciel que j'utilise est censé permettre le partage de dossier, j'ai quand même été obligé d'utiliser ce magnifique logiciel qu'est samba!

Vous aurez besoin de:

* Un système linux avec les dossiers que l'on veut partager, ça marche aussi avec les périphériques. ( moi je tourne sous ubuntu et mes musiques et le reste sont sur un disque dur externe)

* Une machine virtuelle ( moi: Oracle VM VirtualBox, avec windows xp dessus)

En théorie, puisque samba marche sur la plupart des OS on est pas obligé d'être  sous linux mais bon j'ai pas le temps de tester. :P

# Installation:
Pour installer Virtualbox il suffit d'installer le paquet `virtualbox-ose`. Donc soit dans un terminal soit via la logithèque ubuntu. Puis d'installer l'os voulut, je répète que j'ai choisit windows xp mais que ça devrait marcher pour n'importe lequel.

Installer ensuite Samba sur votre ordinateur ( pas sur la machine virtuelle). Normalement vous devriez rencontrer aucun soucis à ce niveau là. Sinon il y a des tas de tutoriels qui pourront vous aider.

# Configuration:

Alors nous voilà donc avec samba, son fichier de configuration se trouve dans `/etc/samba/smb.conf`
On exécute donc la commande sudo vim `/etc/samba/smb.conf` et on se retrouve avec quelque chose dans le genre:

![tuto-1](http://alexrio.fr/blog/wp-content/uploads/2011/01/tuto-1-300x300.png)

La partie qui nous intéresse  se situe après la section `[global]` dans la partie Global Settings, on va y rajouter le nom du dossier partagé entre crochets ( il est totalement fictif, il permettra juste d'identifier les différents partage), puis le chemin, nommé path avec la forme suivante:

`path = /'chemin'`

Pour l'exemple on peut prendre path = /home/transfert/ pour un dossier sur le disque; ou bien path = /media/ pour un périphérique. Ensuite on peut rajouter un commentaire, en écrivant par exemple: comment =  dossier contenant de la musique.
Vient ensuite la partie sur la visibilité du dossier, puisque c'est juste en réseau local on va écrire:


    public   = yes
    writable = yes

Pour pouvoir voir et modifier. Et voilà le fichier smb.conf est prêt à l'emploi. Si vous êtes débutant sous vim, appuyez sur "échap" pour quitter le mode insertion, puis entrez :wq pour sauvegarder et quitter le fichier.
Voilà à quoi ressemble ce que l'on vient d'écrire:
![tuto2](http://alexrio.fr/blog/wp-content/uploads/2011/01/tuto2-290x300.png)

Pour vérifier la syntaxe de votre fichier placer vous dans le dossier /etc/samba puis exécutez la commande testparm smb.conf, elle vous dira si il y a une erreur dans l'écriture, mais pas dans le fonctionnement.

S'il n'y a pas d'erreurs on peut tester le tout dans notre machine virtuelle.

# Test:

Lancez votre machine virtuelle, et si c'est windows exécutez la commande \'votre adresse ip locale' ce qui correspond à \192.168.1.13 pour les gens chez Orange, 192.168.1.7 chez Bouygue.
Dans la fenêtre qui s'ouvrira vous devriez trouver les dossiers partagés, ici Transfert, My Passport et les imprimantes partagées ( par défaut dans le fichier smb.conf).
Vous pouvez désormais accéder à des dossiers de votre disque dur en passant par une machine virtuelle.

# Pour aller plus loin:

Comme dans mon exemple je parlais du logiciel Zune, et que je rédige ce tutoriel pour quelqu'un qui veut s'en servir je vais finir le travail :P

Pour que Zune trouve les dossiers dossiers partagés il suffit de les rajouter en "favori réseau":

![tuto-3](http://alexrio.fr/blog/wp-content/uploads/2011/01/tuto-3-300x221.png)

Suivez l'assistant et rentrez le chemin du dossier qui contient vos musiques/vidéos/musiques ou autre, dans mon cas j'ai fait un raccourci général: \192.168.1.13My Passport, il ne reste plus qu'à rajouter ce dossier dans les paramètres de Zune. ;)

Bien sur il reste encore quelques petites choses à faire, comme configurer les droits, mettre des utilisateurs etc... mais j'ai préféré rester simple, et ne pas faire un énième tutoriel de samba ( j'ai trouvé aucun tuto qui parlait de la machine virtuelle).

Bon et bien j'espère que ce tuto vous sera utile et que je continuerai à poster ici plus régulièrement.
