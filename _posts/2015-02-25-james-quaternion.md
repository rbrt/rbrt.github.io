---
layout: post
title: James Quaternion
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

For the last week and a half I've been working on something tentatively titled

<h3> James Quaternion </h3>

<img src="/images/JamesQuaternionFlightDemo.gif">

I'm trying to create an aesthetic influenced by Star Fox 64, and the game is
sort of evolving as I implement different effects and mechanics. It's been fun,
and my first real foray into doing anything in 3D beyond really short game jams.
To get a pixelated effect, I'm pushing the camera to a 256x256 RenderTexture
which is placed in front of an orthographic camera. This gives me a really blocky
screen for free, and should also be nice for adding other fullscreen effects
down the line.

I decided to spend more time in Blender, and have been making almost all of the
assets for the game using it. The water and land are procedurally generated, but
the ships, lasers, explosions, etc. have all been made in Blender. Right now I'm
using a bunch of materials to colour the individual parts of each model, but I want
to provide vertex colour data to the models and get at that in the shader to save
from having so many materials in a scene.

<h5><i>The player's fighter</i></h5>
<img src="/images/JamesQuaternionFighter.png">

<h5><i>An enemy blimp</i></h5>
<img src="/images/JamesQuaternionBlimp.png">

So far, aside from flying around, you can shoot lasers (both charge shots and
regular shots) and launch seeker missiles. I implemented the laser charge by using
a particle system with a negative velocity so that it emits inwards. A parameter
controls the colour of the charge shot, and will also be tied to damage when damage
is programmed. The missiles are kind of cheating as they just have force applied
and use Transform.LookAt to move towards their target, but the effect works well
enough.

<h5><i>Charge shots and seeker missiles</i></h5>
<img src="/images/JamesQuaternionLaserMissileDemo.png">
