---
layout: post
title: Vertex Painting
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

Last night I started modeling a second car. I picked something less boxy than the
AE86 so that it would force me to spend some time getting the round bits correct.
I still have a long way to go as a 3D artist, but I'm pretty happy with what came
out. The car I decided to model is an NA Mazda Miata:

<img src="/images/2017/Feb/MiataModeling.png">

I learned a few new things this time. One of these was the mirroring tool, to
save me from having to repeat the same actions on either side of the car. Since
cars are almost always symmetrical, they are a great use case for it. However I
learned about this tool at the end of the process, so I'll use it from the start
on the next car. The other thing I learned about was vertex painting. I knew that
you could give vertices colour information, but I assumed that I would have to stack
multiple vertices on top of one another to get different coloured faces sharing the
same vertex. However, it turns out that Blonder will let you select faces and
then paint them how you like. Perfect!

<img src="/images/2017/Feb/VertexPainting.png">

This let me paint various faces of the model in different shades of black. Then
when I bring the model in to Unity, I use a shader to look at the vertex's colour
and convert that to a corresponding colour defined on the material. For the last
model, I was using a texture. I like this approach a lot more. I would like to
determine a cool effect for reflections in the game, maybe just a matcap, but for
now I'm just making all windows and glass light blue. Here's the finished-ish model:

<img src="/images/2017/Feb/MiataSpin.gif">
