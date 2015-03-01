---
layout: post
title: Train Jam: Complete
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

We did it:

<h5><i>Infiniclub</i></h5>
<img src="/images/Infiniclub.gif">

<a href="http://twitter.com/allanlavell">Allan</a> and I, despite being really sick
and sleeping terribly for the duration of the jam (although I guess that describes
anyone who wasn;t in a sleeper car) managed to push out a pretty ridiculous game.
We called it Infiniclub, and the pitch is basically that it's Crypt of the Necrodancer
meets Flappy Bird. We wound up with a playable prototype with standin music and
some very broken mechanics.

I managed to put my recent Blonder skills to good use, making a bunch of dancing
characters and some additional art assets. Everyone was animated in Unity, as I
still haven't ventured into rigging and animating anything in animation software.
We targeted the iPhone, and have a working build on each of our phones where you
swipe in the direction you want to move, but we also put keyboard controls in place
because swiping with a mouse is a huge pain for testing.

The look of the game came together towards the end of the weekend, but was actually
really straightforward. I put a single rotating directional light with a moderate
intensity and white colour in the scene, and then gave essentially everything in the
game a specular material. I tried to pick base colours and specular colours that would
blend nicely together, and even when it didn't work the effect was still cool. What
using the specular material bought us was the effect where everything changes colour
in a strobing motion at the same time. It also adds a great deal of variety to the
colour palette in the scene at any given time.

We also put in a pooling system, and used it to define several different types of
object pools. This lets the game go on forever without needing to instantiate a
whole bunch of new GameObjects (expensive!) and keeps things running smoothly. We also
managed to include (per device) persistent high scores which display on the main screen,
and a system of multipliers and gaining points through collectable items during gameplay.

The big glaring thing we weren't able to get tight was actually enforcing that the player
be interacting with the game to the rhythm of the song. Towards the end of the jam,
we came to the conclusion that Unity's audio timer (AudioSettings.dspTime) diverges slightly
from it's in game timer. We tried to rig up some last minute solutions to compensate for
this (literally, in the last 20 minutes) but were unable to get it down perfect. So for Train Jam,
the player can just tap whenever they please and only needs to worry about maintaining
their multiplier.

Some other notable games included a twin stick jouster where you attack by spinning the
sticks in motion together, a two player game of chicken with a train where the train is
totally random and provides no warning, a 4 player kart racer where each player uses
half of a controller to play, and a racing game where the track is revealed only as players
die by flying off of it. It was a really cool experience, an interesting way to travel,
and definitely worth doing. Now we're all in SF getting ready for GDC tomorrow, staying
at the Mason St Hostel with what seems like everyone else from the train. Here we go.
