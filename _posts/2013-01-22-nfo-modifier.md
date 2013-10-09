---
layout: post
title: nfo-modifier
categories:
- Coding
---
<em>Homonymie, cette article ne traite pas des fichiers utilisés par Windows et son System Information.</em>

##Qu'est ce qu'un fichier nfo et pourquoi en utiliser ?
<p style="text-align: justify;">Les fichiers nfo sont très utiles pour décrire un ou un ensemble de fichiers auxquels ils sont associés. Cela peut aller du simple <span style="text-decoration: underline;">titre + nombre de pages</span> pour un fichier pdf, de la <span style="text-decoration: underline;">liste des codecs</span> et <span style="text-decoration: underline;">bitrates</span> de chaque pistes audio d'un fichier vidéo jusqu'aux crédits d'une <a title="Demoscene sur Wikipedia" href="http://fr.wikipedia.org/wiki/Sc%C3%A8ne_d%C3%A9mo" target="_blank">démo</a>.

Le nfo est donc devenu un standard pour les teams (comprenez les gens à l'origine des fichiers à décrire) qui aiment beaucoup ajouter une touche personnelle à leurs productions. Un «beau» nfo permet de mettre en valeur une team, faire en sorte qu'on se souvienne de leur nom et qu'on s'oriente vers leurs releases ( «productions» ) plutôt que vers celles de teams concurrentes.

##Contenu
Pour faire un «beau» fichier nfo il faut avant tout :

* Un logo, plus ou moins gros, reprenant le nom ou l'acronyme de la team,
* Un cadre autour des informations du nfo
* Que les informations utiles soient structurées et cohérentes

Et tout ça en ASCII-Art. Bien que certains utilisent un simple fichier texte en UTF8 pour encoder les caractères qui composent les «images» c'est du cp437 qu'il faut utiliser.

##Exemples
Si vous essayez d'ouvrir un fichier nfo avec un éditeur de texte classique voici ce que vous obtiendrez :

![Fichier nfo ouvert avec un éditeur de texte ne supportant pas l'encodage cp437.](/assets/2013/01/nfo_error.png)
Fichier nfo ouvert avec un éditeur de texte ne supportant pas l'encodage cp437, ici gedit 3.4.2.

Alors que ce fichier contient en réalité :

![Fichier nfo ouvert avec NFO Viewer 1.11](/assets/2013/01/nfo_no_error.png)
Fichier nfo ouvert avec NFO Viewer 1.11

Le problème est donc de trouver un éditeur de texte supportant cet encodage, sous Windows c'est assez facile à trouver, pour un système basé sur GNU/Linux bien plus dur.

On trouve facilement des viewers permettant d'afficher des fichiers nfo et des programmes permettant de récupérer les <a title="Metadonnées" href="http://fr.wikipedia.org/wiki/Metadata">metadatas </a>d'une vidéo et de les présenter dans un fichier texte ( texte et non nfo ) mais rien pour les modifier.

##nfo-modifier

<figure>
<img src="/assets/2013/01/interface.png">
<figcaption>Fenêtre principale de nfo-modifier.</figcaption>
</figure>

C'est pourquoi je vous présente nfo-modifier, un projet que j'ai débuté il y a quelques mois et que je poursuis quand j'ai du temps libre, malheureusement trop rarement.

Le code source, documenté, est hébergé sur <a href="https://github.com/AlexandreRio/nfo-modifier">github.com</a> ainsi qu'une explication pour compiler, modifier et redistribuer le projet.

Niveau licence, j'avoue ne pas y avoir vraiment réfléchis, une licence de libre modification bien sûr, je partais sur une CC-0 mais ce sera plutôt une <a href="http://creativecommons.org/licenses/by-nc/3.0/fr/legalcode">CC-BY-NC</a>,  je verrai mieux pour la version 1.0.
À terme l'objectif est donc de permettre et de faciliter au mieux l'édition de fichier nfo, pour le moment nfo-modifier permet de lire et écrire des fichiers facilement : implémentation des fonctions classiques du type «Open», «Save», «Save As…» …

En ce moment je travaille sur un système de profils afin de sauvegarder des templates, il suffit de rentrer le motif du header, des motifs latéraux et du footer pour créer le template. Par la suite il suffit de saisir le contenu du nfo et le fichier est générer avec les décorations autour.

J'attends donc d'implémenter cette feature pour sortir une version 1.0, en attendant le code source est bien sur disponible ainsi qu'un exécutable au format jar, donc <span style="text-decoration: underline;">compatible avec tous les systèmes d'exploitation</span>.
Avec la sortie de cette version «stable» je pense aussi mettre à disposition une version packagée en rpm afin de faciliter la distribution.

Bien sur je suis ouvert à toutes demandes d'ajout de fonction ; vous pouvez également reporter les erreurs et bugs sur le <a href="https://github.com/AlexandreRio/nfo-modifier/issues">site du projet</a>.
