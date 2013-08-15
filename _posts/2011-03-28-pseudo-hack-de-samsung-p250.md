---
layout: post
title: Pseudo hack de Samsung p250
categories:
- Astuce
- Tutoriel
type: post
---
Aujourd'hui on va hacker mon portable!

On va utiliser un code qui permet d'accéder à une sorte de menu système qui va permettre de connaitre pleins de truc cool et de modifier 2, 3 choses au passage. :D

Pour commencer on va rentrer ce code comme si on allait appeler quelqu'un:

`*#0206*8378#`

Les chiffres 837 et 8 apparaitront comme ceci: `_` et le `#` final validera le code. Vous devriez vous trouvez dans ce menu:

![](http://alexrio.fr/blog/wp-content/uploads/2011/03/hack_samsung.png)

Alors rapide tour d'horizon des menus (il y a beaucoup de fonctions dont je ne comprends pas l'utilité ):


* Version -&gt; Permet de connaitre: les library disponibles et le TFS Checksum ( utile si on veut changer le firmware).
* H/W test -&gt; La partie la plus utile à mes yeux, en allant dans le sous-menu Audio Settings/MP3 spk/Rx vol. puis en modifiant la valeur du Level 14( le dernier) pour y mettre disons 5000 au lieu de 3000 on obtient un volume sonore bien plus fort au maximum lors de l'écoute d'un .mp3 ( restez raisonnable, une trop haute valeur donnera un son trop saturé). Dans le sous-menu Vib test on peut tester le vibreur...
* Lock state, ben la aucune idée, chez moi il affiche 2 octets, un à 0 et l'autre à 1.
* SIM info. -&gt; beaucoup de sous-menu que je ne comprends pas, mais sinon ça permet de connaitre l'état de la mémoire pour les contacts du répertoire et pour les SMS stockés en SIM.
* Production -&gt; permet de savoir la date de fabrication du téléphone entre autre.
* Text message -&gt; permet de remplir la boite de messagerie d'auto-messages, un peu useless quand même...
* SAT TEST aucune idée pour le moment ( j'ai pas vraiment cherché pour le moment xD ).
* Band selection -&gt; doit permettre de gérer le réseau, j'en sais pas plus.

Cette manip' doit marcher sur d'autre modèle, peut-être chez d'autre constructeur, mais j'ai pas eu l'occasion de le tester.

Si vous avez plus d'info' sur ce hack ou sur le hacking de portable en général hésitez pas à laisser un commentaire. ;)
