---
layout: post
title: DATA GHOST
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

I don't know where the DATA GHOST came from, but once the idea was there, it had
to be made. I made the ghost by creating a cyclical curve in Blonder

<img src="/images/2016/Feb/Blonder.png">
<img src="/images/2016/Feb/BlonderGhost.png">

and then converting it to a mesh. I've got a vertex shader handling the mouth and "feet"
of the ghost, and the trail is a combination of two dense line renderers and a
particle system.

To get the squares to transition into 1's and 0's, I have a single
128x64 texture that has a 1 on one half and a 0 on the other. Initially the particles
are randomly given a vertex colour of either black or white. When the particles
cross a certain point in space relative to the ghost, I blend between a solid colour
and half of the 1/0 texture. I get either a 1 or a 0 by using the particle's vertex
colour to offset the UVs and only grab half of the texture.

<img src="/images/2016/Feb/GhostParticleShader.png">

The background is a scrolling grid rendered in a fragment shader, not much going
on there except for some fog support to display the INFINITE VOID.

The text is appearing on screen by just using randomish offsets in a coroutine to
simulate a typing delay, and moving the cursor image based on the length of text.

<img src="/images/2016/Feb/DataGhost.gif">
