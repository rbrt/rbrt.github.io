---
layout: post
title: Attack Tree
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

I've put in some more work on PK over the last weeks or so, and have been building
systems to help with making content instead of making content. This is the first time
I've really put more than a weekend into a side project, and also the first time
on a side project that I've really taken the time to design something that will scale.
Usually I just want to hack together something that works, and I think that a big
reason I get discouraged when trying to pick up development again is that my codebase...
well, sucks.

The system I made is a tree for managing combos and special moves. I wound up implementing
this as an actual tree of transforms which gets stored as a prefab. Each transform has
a PlayerAttack component, which holds information like:

+ Animations
+ Damage
+ Effects (knockback, stun, etc)

More importantly, it has a list of "next moves". Each of these moves is associated with
a button press and a timing window, and if input that corresponds to any of these next moves
is fed into the attack tree, then the tree is traversed and that attack is invoked. I also
wound up building some editor tools to help modify and copy the attack tree and to make new
segments. The workflow is straight forward, and once the animations and script for an attack
exist, it's pretty quick for me to add it to the tree.

This has been pretty fun because I really like making tools and systems, and I have something
that, despite being simple, feels good and like something I want to iterate on and extend. The
downside to spending time on these aspects though is that content-wise, I don't have much to
show. My plan for the next short while is to spend some time trying to make a short level and
seeing if I have something fun on my hands. If it feels like there's something there, then
it's time to start adding background assets and new enemies, then get back to systems and moves.

In closing, here is a jab-jab-cross combo in action:
<img src="/images/throw.gif">
