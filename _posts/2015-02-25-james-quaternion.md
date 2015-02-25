---
layout: post
title: James Quaternion
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

For the last week and a half I've been working on something tentatively titled <i>James Quaternion</i>.

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

<h5><i>An enemy blomp</i></h5>
<img src="/images/JamesQuaternionBlomp.png">

So far, aside from flying around, you can shoot lasers (both charge shots and
regular shots) and launch seeker missiles. I implemented the laser charge by using
a particle system with a negative velocity so that it emits inwards. A parameter
controls the colour of the charge shot, and will also be tied to damage when damage
is programmed. The missiles are kind of cheating as they just have force applied
and use Transform.LookAt to move towards their target, but the effect works well
enough.

<h5><i>Charge shots and seeker missiles</i></h5>
<img src="/images/JamesQuaternionLaserMissileDemo.gif">

I implemented a shield by wrapping the fighter in a low poly sphere and modified
Unity's transparent shader to produce three ripples based on two offset values.
Whenever the shield gets hit, the shield gets rotated to face the point of impact,
and then a coroutine quickly lerps the two values to produce a shield ripple effect.
I don't cull the front or back faces, so that you can see the shield ripples all the time.
I also implemented a boost which is pretty straightforward, but I made the boost fire in
Blender and have the engine trails changing colour. I was trying to find a way to
modify Unity's TrailRenderer Colour array, but it doesn't seem to be possible without
editor scripting. (The only way I could get this to work was with the PGJ's <a href="http://forum.unity3d.com/threads/trail-renderer-colors-c.54162/">post</a>)
This is a bummer because the gradual altering of each element of the array looked a
lot better than affecting the material all at once. Ah well.

<h5><i>Shield and boost</i></h5>
<img src="/images/JamesQuaternionShieldDemo.gif">

Over the weekend, I implemented water as well which was a lot of fun. I decided
to do it using Gerstner waves from this
<a href="http://graphics.ucsd.edu/courses/rendering/2005/jdewall/tessendorf.pdf">paper's</a>
section on "Practical Ocean Wave Algorithms". The equation for generating waves involves
summing a series of waves with a few parameters that allow you affect frequency, amplitude,
direction, and (cool but not used in my case) curl of the wave. A single wave looks
like this:

<h5><i>Gerstner Wave</i></h5>
<img src="/images/GerstnerWave.png">

And it generalizes to this:

<h5><i>Summation of Gerstner Waves</i></h5>
<img src="/images/GerstnerGeneralized.png">

I implemented that in a vertex shader which gets applied to a flat shaded procedurally
generated plane, which looks like this:

<h5><i>Oooo, water...</i></h5>
<img src="/images/JamesQuaternionWaterDemo.gif">

Which admittedly is probably pretty simple and could be accomplished with a much less
involved shader, but whatever, this was fun to write. I really want to be recomputing
face normals on the fly so that the colours change, but I don't know of any way to do this
without using geometry shaders, which I can't do in Unity on OSX with an integrated
graphics chip. My assumption here is that I would be able to get information about the
current triangle in the geometry shader, as opposed to trying to figure that out in
a vertex shader which has no knowledge of the other vertices. I might write this on
a windows box or my iMac at work just to see how it looks. Also, if you crank up the
poly count and parameter values, then you get some big rolling waves:

<h5><i>Big old waves</i></h5>
<img src="/images/JamesQuaternionBigWaves.gif">

I've also been working on an effect to distort the area underneath the player. It
works by passing information about the player's position into the vertex shader, when
the player is flying lower than a certain height. A triangle is projected onto the mesh,
which grows as the player gets closer. Inside this triangle, the waves are distorted
at a different rate than the rest of the waves, sort of making it look like the
engines are pushing the waves aside. I haven't quite nailed this effect down yet
and it's especially jarring at the back of the trail, but at present it looks like this:

<h5><i>Wave distortion in relation to the player</i></h5>
<img src="/images/JamesQuaternionWaveDisplacement.gif">

Anyway, more to come.... at some point!
