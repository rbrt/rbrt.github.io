---
layout: post
title: Fun With Tool Development
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

I really like making tools. The most experience I have with this is in the context
of editor scripting in Unity, but it's something I've been doing whenever it makes
sense. I've found that I really enjoy tool development because it's wonderful to
click a button or run a command and have a tedious process completed quickly and
automatically. But since developing tools for production, I've also found another
aspect which I really enjoy: the quick feedback loop.

In my situation, the tools are put into use almost instantly, because they're
usually developed to solve a problem currently facing the team. Sometimes, the
tools are put into use before they're even really completed. This leads to a
process where I'm getting feedback on what is and isn't useful, and what would be
better right away. To contrast this with the other development I do at work, aside
from limited playtesting, we have had no outside eyes on our game, and thus no
feedback. I find it immensely satisfying to know that people are using things I've
created, and with tool development, that occurs quickly and often.

Here are some tools I've made over the last year that have been fun to implement:

<h4>Automatic Navmesh Generation</h4>

We have a large, streaming world comprised of many scenes. (I want to take a moment to plug
<a href="http://www.sectr.co/">SECTR</a> which has helped out a lot!) Unity has a limitation
(which looks to be addressed in the upcoming Unity 5) that prevents us from streaming
in navmeshes, so the solution is to have one large navmesh. Importing all the relevant
geometry is time consuming, annoying, and frequently causes the poor 32-bit application
to crash. To solve this, I wrote a tool which gradually imports each scene and deletes
everything which will not be included in the navmesh (see: not marked navmesh static).
At every stage of the process, the temporary scene is saved and the import progress is
stored in a scriptable object. This allows us to resume from where we left off in the
event of a crash. Once all of the scene contents have been imported,then the
giant navmesh is baked.

<h5><i>Selecting what to include in Navmesh</i></h5>
<img src="/images/AutomateNavmeshMenu.png">

<h5><i>End result</i></h5>
<img src="/images/BakedNavmesh.png">

Before having this tool, one of our devs would have to be tied up for the duration of
each import, as well as the final bake. Each manual import of each scene was
essentially a roll of the dice, as it was very likely that Unity would crash (and
more so with each successive scene) especially considering that all GameObjects were
kept around. Deleting all of the non-essential objects helped out considerably.

The only parts of this process that are not automatic are clicking the buttons to
invoke the import and bake, and then reverting all changes (except the new navmesh)
in mercurial. Reverting changes in source control is somewhat heavy handed, but it's
quick, foolproof, and allows us to do the very destructive operation of deleting
all non-essential objects safely.


<h4>Automatic Creation and Updating of Mecanim Animation State Machines</h4>

We have a great deal of assets whose names are just hashes, and these need to be
associated with animations. We had hoped that we could do something at runtime
using override controllers, but found that in order to play things smoothly, on
demand, and without crashing, we needed to have the relevant animations already
set up in a state machine. To this end, I created a tool to build these large
state machines, which look like this:

<h5><i>I tweeted this on the day of writing the tool</i></h5>
<img src="/images/AnimationStateMachineTweet.png">

They are gross to look at (and actually, the states are all on top of eachother.
I spread those out manually for the screenshot) but are basically never used by
a developer directly; all invokation is done by hash reference through code. I
has so much fun with this because I got to use reflection (<3) to get at all of
the underlying functions to construct the state machines. First I had to poke
around for a bit to see how things work and what was available, and then I started
on generating state machines. Since we don't need transitions defined (we
just crossfade) this was pretty straightforward, but fun nonetheless. The tool is
able to generate a new layer (so as not to interfere with the other states on an
AnimationController) and also able to update an existing layer when new animations
are added. It took something that would've been really tedious and error prone,
and made it into a development step that runs in a few seconds.
