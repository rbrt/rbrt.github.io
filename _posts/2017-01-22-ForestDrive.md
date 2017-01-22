---
layout: post
title: Forest Drive
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

This weekend I've been getting over a pretty rough cold, but I've just been
continuing to work on <i>Mountain Drift</i>. For whatever reason, I've been
really motivated to keep working on this project, so I decided to keep riding that
momentum.

Originally for my smoke, I was using sphere mesh particles with an additive particle
shader, and this was killing performance all the time. It was fine for a first pass,
but I needed to do something about it. In keeping with the low poly art style, I
hopped into Blonder and made a smoke mesh:

<img src="/images/2017/Jan/SmokeMesh.png">

Because this has a decent shape to it, I can use a shader that doesn't do any alpha
blending. As soon as I made this change to my smoke particles, performance was no
longer a problem. I think I like the resulting effect more too, but this probably
isn't the final pass.

<img src="/images/2017/Jan/NewSmoke.gif">

I also extended the track and added a finish line. At the base of the mountain,
there is the beginnings of a forest. I really want to look into various solutions
for creating nice backgrounds; I'd like to have a distant city, mountain ranges,
or a seemingly infinite forest and none of those are things I've tackled before.
For now, this is what the finish line looks like:

<img src="/images/2017/Jan/Finish.gif">
