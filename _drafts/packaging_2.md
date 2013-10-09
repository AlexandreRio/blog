---
layout: post
title: Packaging Partie 2 — Automatisation et multi plateforme
categories:
- Coding
- Tutoriel
---

## Rappels

Dans mon article précédent nous avons vu entre autres les différentes étapes du packaging et la structure globale d'un SPEC file.

Pratique pour un usage personnel ou pour dépanner quelqu'un mais pas du tout adapté pour distribuer à grande échelle un logiciel.

La mauvaise solution serait de créer une VM pour chaque distribution et gestionnaire de paquets, bien entendu il existe une solution bien plus simple.

## OpenBuild Service

OpenBuild Service ( abrégé OBS par la suite ) est un ensemble d'outils qui va nous permettre de faire du packaging multi architectures et multi distribution de manière automatisée.

OBS est OpenSource et disponible sous licenese GPL, vous pouvez donc l'installer sur votre propre serveur mais pour des questions de : performance ( le packaging demande beaucoup de ressource) et de simplicité c'est l'OBS hébergé par [Novell](http://novell.org) qui sera utilisé, à savoir [build.opensuse.org](http://build.opensuse.org).

### Préparation

Puisque l'on utilise un OBS public il n'y a rien à instaler, il suffit de se créer un compte puis de créer un projet vide.

On pourrait se contenter d'uploader une archive contentant les sources de notre programme et notre .spec mais il y aurait que peu d'intérêts, à part proffiter de la puissance de calcul des serveurs.

Capture de l'interface du projet, statuts des builds sur la droite etc…

![project files](/assets/2013/09/project_files.png)

### Récupération des sources

Supposons le cas suivant :

* Les sources de mon programme sont hébergées sur un serveur GIT,
* J'ai déjà écrit mon spec file

Si vous n'arrivez à avoir un spec file fonctionnel reportez-vous à l'article précédent.

Puisque l'on ne va pas héberger directement nos sources sur l'OBS il faut lui dire où et comment les récupérer.

#### _service

On va créer un fichier `_service` qui contiendra cette marche à suivre.

Un exemple simple de fichier `_service` :

{% highlight xml %}

    <services>
    <service name="tar_scm">
      <param name="scm">git</param>
      <param name="url">https://github.com/seandepagnier/climatology_pi.git</param>
      <param name="filename">OpenCPN_climatology_pi</param>
    </service>

    <service name="recompress">
      <param name="compression">bz2</param>
      <param name="file">*OpenCPN_climatology_pi*.tar</param>
    </service>

    <service name="set_version"/>
    </services>

{% endhighlight %}

La structure est claire, le service `tar_scm` va récupérer les sources depuis le serveur GIT puis le service `recompress` va en faire une archive.

À noter qu'il faut que le paramètre `file` du service `recompress` corresponde au fichier `Source` indiqué dans votre spec file.

Pour ne récupérer qu'un sous-dossier il suffit de rajouter la ligne suivante après la propriété `url`.

    <param name="local_path">sous/dossier</param>

####Les statuts

Désormais si vous uploadez votre fichier `.spec` et le `_servie` le statut passera de `broken` à `scheduled` puis `building` et si tout se passe bien à `succeeded`, sinon à `failed`.
BSLight et OBSLight-gui

![build status](/assets/2013/09/build_status.png)

La transition entre ces états peut demander un peu de temps, il dépend de la charge du serveur, sur build.opensuse.org il est en général de l'ordre du ¼ d'heure.

Les cas d'erreur les plus fréquents et leurs raisons la plus fréquentes :

<table>
  <tr>
    <td>failed</td><td>Votre spec file contient une erreur.</td>
  </tr>
  <tr>
    <td>unresolvable</td><td>Une dépendance ne peut pas être résolue, une faute de frappe ou la dépendance porte un autre nom en fonction de la distribution cible.</td>
  </tr>
  <tr>
    <td>broken</td><td>Il manque un fichier.</td>
  </tr>
</table>

### Paramètrage des targets

## OBSLight et OBSLight-gui
