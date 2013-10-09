---
layout: post
title: Packaging Partie 1 — Les bases
categories:
- Coding
- Tutoriel
---

## Introduction

L'opensource c'est bien, ça offre énormement d'avantages, les licences libres c'est encore mieux, je ne m'étendrais pas plus sur ce sujet.

Le développement de forges «sociales» qui intègrent, un logiciel de version de contrôle ( git ou svn ), un bugtracker, un forum ou un wiki et une joli page d'accueil et ce pour chaque projet ont permis le développement de nombreux projets, certains aboutissant, d'autres sont laissés à l'abandon après quelques semaines.
La ( une ? ) raison à cela est que beaucoup de projet commence par du code, puis code encore et… c'est pratiquement tout. Peu de temps passer à documenter et encore moins à distribuer.

Pour la plupart des projets opensource indépendants la distribution se résume à :
    «Les sources sont là, démerdez-vous !»

L'utilisateur doit donc :

* Lire le fichier README pour comprendre comme le projet est structuré,
* lire le ficiher INSTALL pour voir comment la compilation va se passer ( cmake, make, un configure avant ? ),
* faire plusieurs tentatives parceque les bonnes dépendances ne sont pas installées pour
* finalement installer le programme sur son système


C'est donc un process' plutôt long, surtout parce qu'il peut être réduit à :

* Choisir la version correspondant à notre système, distribution et architecture,
* installer le programme

La solution est donc d'utiliser des paquets, des archives compressées contenant le programme déjà compilé.
Cette méthode est utilisée par la plupart des distributions pour ces paquets «officiels»

Les paquets sont stockés dans des dépôts que l'on ajoute ou retire à l'aide d'un gestionnaire de paquets, ils seront consultés lorsque l'on voudra installer un nouveau paquet.
Les gestionnaires de paquets les plus utilisés sont APT ( pour Debian et ses dérivés ), Yum ( pour Fédora et ses dérivés ) et ZYpp pour OpenSuse, on doit aussi utilisé un programme pour les installer mais je ne vais pas rentrer trop dans les détails.
Les formats de paquet les plus répendus sont .deb et .RPM, je connais mieux les RPM mais puisque je vais rester plutôt théorique cela ne devrait pas poser de problèmes.

## Utilisation

Pour interroger sa liste de dépôt à la recherche d'un paquet nommé foo on fera par exemple :
    aptitude search foo
    yum search foo
    zypper search foo
	( pour des raisons de commodité je n'utiliserai plus que zypper dans la suite de l'article, des équivalents existent pour les autres gestionnaires de paquets )

Une description d'un paquet peut être obtenue avec un `zypper info foo` et pour finir un `zypper install foo` installera le paquet, je reviendrai plus tard sur comment se passe cette partie, en vérifiant avant qu'il _peut_ être installé.

## Les dépendances

Une dépendance est un paquet nécessaire au fonctionnement d'un autre paquet, l'exemple le plus simple est si notre paquet est une application Java, le paquet à besoin d'un Java Runtime Environment.
Si le gestionnaire de paquet n'en trouve pas sur le système il ferait une recherche dans la liste de ses dépôts, si un paquet fournit un JRE ( on dit qu'il provides ) il sera installé en plus, si aucun paquet n'est trouvé l'installation est annulée. Sauf choix de l'utilisateur un gestionnaire de paquet ne cassera pas une dépendance.

## Structure d'un paquet

Concrètement un paquet est simplement une archive compressée et des méta-données.

### Méta-données

Les méta-données seront lues par le gestionnaire de paquets, il peut s'agir par exemple du :

* nom du paquet,
* descriptif,
* numéro de version,
* de la licence,
* des dépendances,
* groupe auquel appartient le paquet, s'il s'agit d'une application, d'une bibliothèque etc…
* …

### Fichiers

Les fichiers compilés qui seront installés, sous la forme d'une arborescence, on peut imaginer le contenu suivant :

    ./usr/bin/foo
    ./usr/share/foo/doc/default.conf

Ces fichiers seront copiés tel quel sur le système et cette même liste de fichiers sera supprimée lors de la désinstallation.
On peut noter qu'il n'est pas possible de placer ses fichiers n'importe où, il faut que le package ait la permission, en particulier lorsqu'on package un plugin qui doit s'ajouter dans le dossier d'un programme hôte, si lors du packaging le lien de dépendance est bien établi l'installation pourra avoir lieu.

## Packaging : la pratique

Maintenant que nous avons vu comment était fait un paquet et comment s'en servir, il reste à voir comment en faire !
Tout d'abord je tiens à préciser que _ce n'est pas compliqué_ à partir du moment où vous avez déjà compiler vous même un programme récupéré sur internet et que vous avez lu les paragraphes précédents.

### Les outils

Avant de pouvoir commencer à faire des paquets il faut d'abord préparer son système, installez le paquet rpmbuild ou documentez-vous sur les paquets nécessaires en fonction de votre distribution, par exemple sous Fedora il faut installer : @development-tools et fedora-packager.

Il ne reste donc plus qu'à écrire le fichier spec, qui décrit la marche à suivre du packaging, et à créer l'arborescence.

### L'arborescence de travail

Placez-vous dans un nouveau répertoire et faites la commande suivante :

`mkdir SPECS SOURCES BUILD BUILDROOT RPMS SRPMS`

    SPECS      Contient le fichier spec, qui décrit comment le packaging va se passer
    SOURCES    Contient les sources du programme voulu
    BUILD      Contient les sources compilées
    BUILDROOT  Contient les fichiers compilés sous forme d'une arborescence
    RPMS       Répertoire de destination des paquets que l'on va créer
    SRPMS      Répertoire de destination des sources du programme qui seront packagée

### La méthode

On va maintenant passer à la rédaction du spec file, c'est là le plus compliqué puisqu'il vaut mieux bien connaître le programme que l'on package pour avoir le paquet le plus propre possible.

On retrouvera 3 types d'éléments :

* les tags fournissant de l'information, exemple: «Name: Mon-paquet»,
* les variables ( ou macros ), souvent utilisées pour les emplacements, exemple: «%{buildroot}»,
* les sections, représentent les étapes du packaging, exemple: %install

#### Informations sur le paquet

Une partie du spec file contient des informations relatives au paquet que l'on est en train de créer.
La première partie contient au minimum les tags suivants :

    Summary       Résumé du paquet, affiché lors d'une recherche
    Name          Nom du paquet
    Version       Numéro de version des sources que l'on package
    Release       Numéro de version des sources que l'on package
    BuildRoot     Emplacement utilisé lors de la compilation et l'exécution des scripts, en général quelque part dans /tmp
    Group         Groupe auquel appartient le programme, Application par exemple
    URL           Site du projet, où l'on peut télécharger les sources du programme et obtenir plus d'information
    Distribution  Système pour lequel le programme est prévu
    License       License sous laquelle est distribuée le programme
    BuildRequires Programme nécessaire lors de la compilation du programme, il est possible de préciser une version minimale
    Requires      Programme nécessaire à l'exécution de programme, ici aussi on peut préciser une version
    Source        Emplacement des sources du programme, un répertoire ou une archive


On peut aussi utiliser `Patch:` pour définir l'emplacement d'un éventuel patch à appliquer.

Les tags `BuildRequires` et `Requires` peuvent être utilisés plusieurs fois à l'indentique; les tags `Source` et  `Patch` doivent être numérotés s'ils sont répétés, `Patch0, Patch1 …`.

Deux macros sont utilisées pour fournir de l'information, directement après les différents tags :

    %description
    Description du paquet, affiché par zypper info


Et en toute fin du fichier spec la macro %changelog pour garder une trace de l'évolution du fichier :

    %changelog
    * Tue Jul 30 2013 Alexandre Rio <mail@host.tld>
    - fix something

    * Tue Jul 23 2013 Alexandre Rio <mail@host.tld>
    - package upstream source 1.0


#### Les sections

Les sections sont très proches de l'arborescence vue tout à l'heure puisqu'à chaque changement de section l'on change de répertoire de travail.


    %description
    %prep
    %build
    %test
    %install
    %clean
    %files
    %changelog

Les sections `%test` et `%clear` sont optionnelles.
`%description` et `%changelog` ont déjà été vus précédemment, ils ne seront pas traités dans cette partie.

Le `%prep` prépare les sources : extrait l'archive, applique les patchs…

Le `%build` compile les sources, on placera donc ici les commandes que l'on aurait tapées pour une installation classique.


    %build
    mkdir build
    cd build
    cmake ../
    make


`%test` est assez clair, c'est prévu pour y lancer un `make test` ou équivalent.

Le `%install` fait à peu près la même chose qu'un `make install` classique sauf que là les fichiers ne sont pas collés sur le système mais dans le répertoire `BUILDROOT`.

`%clean` permet de nettoyer le `BUILDROOT`, on l'utilise en général de cette forme :


    %clean
    rm -rf %{buildroot}


Et il ne reste plus que la section %files, ici on va lister les fichiers contenu dans le répertoire `BUILDROOT` que l'on veut inclure dans le package que l'on va créer. On préfèrera utiliser des macros plutôt que les chemins en durs.
Par exemple pour garder tous les executables produits :

`%{_bindir}/*`

Nota : Attention à votre valeur de `%{_prefix}`, elle peut valoir /usr/local/ et non /usr/.

### Packaging

Une fois que le spec file est écrit il ne reste plus qu'à lancer la procédure.
On se place dans le répertoire `SPECS` et on lance le packaging :

`rpmbuild -ba program-name.spec`

L'argument `-ba` lancera les section `%prep`, `%buid` et `%install` puis fera le package compilé et le package des sources.

## Test

Si vous souhaitez avoir un jour votre package dans un dépôt officiel il faudra que sa syntaxe respecte les normes. Pour tester la validité d'un spec la commande `rpmlint` est à utiliser.

`rpmlint package-name.spec`

## Liens utiles

* [Fedora Wiki](https://fedoraproject.org/wiki/How_to_create_an_RPM_package)
* [Build OpenSuse](https://build.opensuse.org/), où vous pouvez trouver beaucoup d'exemple de spec file.
* Et bien sur les manuels de `rpmbuild` et `rpmlint`.

## Allez plus loin

Dans cet article le packaging le plus «simple» a été vu, dans l'article suivant nous verrons comment :

* permettre une récupération depuis un serveur git,
* faire du packaging pas à pas,
* produire des packages pour différentes plateformes et architectures,
* travailler dans une «chroot jail»
