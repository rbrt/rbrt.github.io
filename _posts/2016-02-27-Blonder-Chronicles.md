---
layout: post
title: Blonder Chronicles
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

I'm pressing on with trying to figure out Blonder a bit more. I've been making a
prototype for a game lately (which I'll probably post about soonish -- I want to
have it ready for the next <a href="https://www.facebook.com/groups/halifaxgamecollective/">Halifax Game Collective</a> meetup.)
After I got basic gameplay out of the way, I decided to start making a character
because as it stands, everything in my game is a cube.

So I hopped into Blonder and modelled, rigged, and animated a humanoid-ish character:

<img src="/images/2016/Feb/BlonderAnimation.png">

I gave it 6 animations; an idle, a run, a jump, a fall, a landing, and one for
taking damage. I kept the starting and ending frames mostly uniform with the states
that the animations could transition in and out of so that blending would go nicely.
I then brought it into Unity and made a pretty straightforward state machine to
control it, and set up the transitions to blend appropriately.

<img src="/images/2016/Feb/StateMachine.png">

I already have to code dictating all of these behaviours done up, so hooking my
player controller up to the animator should be pretty straightforward. From here
I want to make an enemy or two, and then start working on the terrain and scenery
for the game. As I have the basic game loop established (menu, gameplay, death)
and a scoring system, I think that adding some pretty basic art will help it feel
a lot better. The following gif doesn't show all the animations, but it shows the
transition from running to jumping to falling to landing:

<img src="/images/2016/Feb/RunJumpFall.gif">
