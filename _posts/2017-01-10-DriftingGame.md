---
layout: post
title: Drifting Game
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

I've been playing a lot of Forza Horizon 3 since it came out last year, and it's
a total blast. The events in the game aren't so great, but just driving around
the "mini Australia" they've created is both entertaining and relaxing. What
I've really come to enjoy is drifting around the mountains and hills. The sound
of tires squealing, the trail of smoke, and the feeling of controlling the car
while it gets sideways is something I've been coming back to for months.

I wanted to try and capture that feeling and make a game that was about only that.
I started off by looking into Unity's standard car asset. I was able to get some
interesting results after several hours of messing around with physics settings;
four wheel drive with reduced friction on the rear wheels seemed the let the car
slide around a lot. Unfortunately, even at the best settings I managed to find,
I found that the settings weren't general. What worked for sliding would lead to
a car that could barely accelerate in a straight line. It would also be prone to
spinning out. I attempted to change between settings on the fly, but the handling
was still not something I was happy with.

Before continuing on any further, I had to make a little car and a mountain scene
to drive it around in. I wound up making a track by extruding a mesh along a path
in Blonder and applying a road texture to it, then I surrounded it with a bunch of
mountains.

<img src="/images/2017/Jan/Mountains.png">

After that, I took a stab at making a low poly AE86:

<img src="/images/2017/Jan/AE86.png">

Next up I tried slapping a rigidbody on my car and applying forces to it manually.
I found that applying torque to turn was heavily dependent on how much contact the
collider had with the ground, but applying forward momentum worked consistently well.
The solution I wound up utilizing was to apply force to the rigidbody, but then
to bypass physics for rotation and rotate the transform directly.

This actually feels pretty good, and the car can be adjusted to feel pretty different
(without being out of control) by tweaking max speed, acceleration, and turn speed.
Most importantly, the car is really drift-happy, which is exactly what I wanted.
I made a build and put it on my phone, and even though there wasn't much to it,
it made me feel the same way I felt sliding around in Forza. I'm going to keep at
it.
