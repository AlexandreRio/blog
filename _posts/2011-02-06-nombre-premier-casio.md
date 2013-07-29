---
layout: post
title: Nombre Premier Casio
categories:
- Coding
tags: []
status: publish
type: post
published: true
---
Bonjour!

Aujourd'hui je vais vous montrer un p'tit programme pour calculatrice de type Casio (je l'ai coder pour ma Graph 100+) qui vérifie si le nombre entré est premier ou non. Si vous avez des idées d'amélioration dites le moi. ;)

{% highlight bash %}
"NOMBRE"?→A
ClrText
If A=2
Then Locate 1,2,"NOMBRE PREMIER."
Stop
IfEnd
Int (√A)+1→B
Int (√A)→E
Int (A/2)→J
(A/2)→K
If J=K
Then Locate 1,2,"NON PREMIER"
Stop
Else
Locate 4,2,"/ DU TEMPS RESTANT MAX"
While B≠1
B-1→B
A/B→C
Int (A/B)→D
Locate 1,2, Int (((E-B)/E)x100
If C=D
Then If A=1
Then 2→B
IfEnd
If B=1
Then Locate 1,3,"NOMBRE PREMIER."
Else Locate 1,3,"NON PREMIER."
Locate 1,4,B
Locate 1,5,C
IfEnd
Stop
IfEnd
WhileEnd
IfEnd
{% endhighlight %}
