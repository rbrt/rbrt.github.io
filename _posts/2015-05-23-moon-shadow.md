---
layout: post
title: Moon Shadow
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

My friend (<a href="https://twitter.com/macbooktall">Connor Bell</a>) has been
working on a really cool iOS app lately called Moon Shadow. Following along in a
pretty logical manner from his last project <a href="http://www.glitchwizard.com/">Glitch Wizard</a>,
Moon Shadow lets you apply a whole bunch of glitch effects to video in realtime.
You can also take still images, and the results can look something like this:

<img src="/images/moonshadow1.JPG">

What's been really rad about it though is that he's asked a bunch of friends from
in and out of Halifax to write shaders for it. The results have already been awesome
and it's going to be incredibly fun to play around with once he releases it to the public.
I've been getting Test Flight builds and having a bunch of fun with them. Anyhow, I
wrote two shaders for it that I'm pretty into, although the second one is a bit
too chaotic. The source (and examples) for them are up on my ShaderToy account.
Actually, they're all that's on my ShaderToy account.

The first one I wrote is this goofy thing that makes the screen collapse in on itself:

<h5><i><a href="https://www.shadertoy.com/view/Mt23zG">Source</a></i></h5>
<img src="/images/moonshadow3.gif">

It works by converting all the points in UV space (0-1) to values between -1 and 1.
From there I just find the direction vector from the current pixel to (0,0) and move
the points along that line, repeating when they "pass" the center or fall off the
edge of the screen.

The really noisy one I wrote is this spirally dealie:

<h5><i><a href="https://www.shadertoy.com/view/Ml2GzG">Source</a></i></h5>
<img src="/images/moonshadow2.gif">

To be honest I'm not totally sure what's up here, I got it working through a bunch
of trial and error. Roughly though, what's going on is a conversion from UV space to
values between -1 and 1. From there I find the angle between the line formed by
the current point and (0,0), and the line from (0,0) to (1,0). I also get the
magnitude of the vector of the current point. I use the magnitude of the vector along
with the sine function to distort the current point along the line formed from the
center of the screen to the current point. This results in several wavy patterns radiating
from the center. So maybe I do kind of know what's going on? Cool.

Anyway Moon Shadow is sick and it was really fun to have an excuse to write wonky shaders
beyond just making something silly to look at. It's been sick to see what other people
have been doing with them, and I've had a blast playing around with different combinations
of shaders that everyone wrote.
