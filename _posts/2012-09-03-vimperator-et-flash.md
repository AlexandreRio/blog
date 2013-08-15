---
layout: post
title: Vimperator, Flash et VLC
categories:
- Astuce
type: post
---
Bonsoir !

Depuis quelques temps j'ai des problèmes avec le plugin flash de Firefox, outre les nombreux plantages ( oui je troll ) sur certaines vidéos je me retrouve avec un filtre bleu, certes le résultat est cocasse mais vite gênant.

Il se trouve que j'utilise quotidiennement Vimperator, un autre plugin Firefox permettant d'utiliser son navigateur avec des contrôles proches de ceux de l'éditeur Vim. Puisque trop peu de vidéo sont disponibles en HTML5 utiliser VLC ( ou n'importe quel lecteur multimédia supportant un flux réseau ) me semble être un bon compromis et bien sûr Vimperator va nous éviter de devoir : ouvrir VLC, aller dans "Media/Open Network Stream" pour y copier/coller l'url de la vidéo.

Pour ce faire, une fois sur la page de la vidéo voulue, il suffit de faire :

`y:! vlc ^V`

Rapide explication :

'y'  copie l'url courante

':!' lance une commande externe

'^V' ou 'Control-V' va "coller" l'url de la page voulue

MàJ : Après quelques utilisation je me suis rendu compte que certaines vidéos se lancent en HD 1080p par défaut, pour éviter ça il suffit de rajouter

`\&fmt=X ( sans ce \ Vimperator n'en tiendra pas compte )`

Où X correspond à la qualité voulue, voilà la liste possible :

    fmt=0 → flv: 320×240 (flv1) / mp3 1.0 22KHz (identique à fmt=5)
    fmt=5 → flv: 320×240 (flv1) / mp3 1.0 22KHz
    fmt=6 → flv: 480×360 (flv1) / mp3 1.0 44KHz
    fmt=13 → 3gp: 176×144 (mpg4) / ??? 2.0 8KHz
    fmt=17 → 3gp: 176×144 (mpg4) / ??? 1.0 22KHz
    fmt=18 → mp4: 480×360 (H264) / AAC 2.0 44KHz
    fmt=22 → mp4: 1280×720 (H264) / AAC 2.0 44KHz
    fmt=34 → flv: 320×240 (flv?) / ??? 2.0 44KHz (valeur par défaut du lecteur : 360p)
    fmt=35 → flv: 640×380 (flv?) / ??? 2.0 44KHz
    fmt=37 → mp4:1920×1080 (H264) / AAC 2.0 44KHz

On obtient donc la ligne suivante :

`y :! vlc ^V \fmt=34`

Un exemple pour mieux se rendre compte :

`!vlc http://www.youtube.com/watch?v=lC1j5nyMXLM\&fmt=34`

Et bien sur pour automatiser tout ça : une macro !

Faites un <em>:map é y.! vlc \&fmt=34</em> ( remplacer le é par la touche de raccourcis voulue ), puis un <em>:mkv</em> pour sauvegarder la macro ou copier simplement la ligne suivante dans votre fichier <em>.vimperatorrc</em>, à la racine de votre répertoire :

`map é y.! vlc\&fmt=34`

Voilà voilà, j'espère que cette petite astuce sera utile à quelqu'un ou qu'au moins elle aura montrer la puissance et la simplicité de vimperator. À bientôt ! ;)
