---
layout: post
title: Car Selection
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

As it stands right now, there is a stub scene for every state in my game's flow.
At the very least, an empty scene is loaded and a transition occurs, but I've started
adding some functionality to those stub scenes as well. Today I spent some time
fleshing out my car select screen:

<img src="/images/2017/Feb/CarSelect.gif">

Unfortunately I only have one car, but it's still cycling through the list and
should work fine as more cars are added. To rig that scene up, I made more use of
my recording system and added some pause/resume functionality to the playback. I
just recorded the car doing a drift on an isolated stretch of track, found a good
point to pause it at, and made that the point where cars will stop to be displayed.
Pulling back a bit, you can see what cycling through the cars actually looks like:

<img src="/images/2017/Feb/CarSelectTop.png">

I also started work on a background setup. The way this works is I have a camera
which culls everything that isn't on my "Background" layer, and my regular camera
can't see anything on that layer. The background camera is drawn first, and then
the regular gameplay only clears on depth and draws over it. The background camera
also rotates in sync with the gameplay camera. Using this setup, I'll place a bunch
of things floating in the sky somewhere:

<img src="/images/2017/Feb/BackgroundSetup.png">

Right now it's just some water I made awhile ago and a giant sun, but it's easy
enough to add more things and have different contents for different levels. This
is how the setup appears in game:

<img src="/images/2017/Feb/Background.gif">
