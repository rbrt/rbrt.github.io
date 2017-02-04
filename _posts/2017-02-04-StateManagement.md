---
layout: post
title: State Management
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

Mountain Drift is now getting to the point where I need to handle transitions between
different game states, and the operations to do so are varied and non-trivial.
I'm also finding that as I develop different parts of the game, it's good to be
able to start in any of my scenes instead of having to navigate to them through
normal game flow. Unfortunately, that causes issues with instantiation of UI in
different states, and concerns with what has and has not been initialized.

To help with both of these problems, I decided to write a state management backend.
I've done this a few times before, mainly for projects at previous jobs, and I
feel like I have a pretty good handle on it at this point. The core of the system
is that there are several defined states, and transitioning between them invokes
a set of functions. This operation tries to be as atomic as it can, so there can
be a guarantee of nothing unexpected occurring during a transition.

Previously, I've worked under the idea that a state transition means loading a new
scene. This works well enough, but it leads to some awkward hacks and entangled
code when you don't necessarily want to load a new scene, or when unloading the
current scene causes problems. The main design flaw that enforced this limitation
was that my state manager was also my loading controller. In this implementation
I've decomposed the two into separate classes. Now, a transition can load a scene,
but it isn't forced to do so.

To facilitate this, I've defined several states, and created a StateTransition
struct. The struct defines what states can be transitioned to from the current
state, and also has three functions. `transitionFromAction` is what sort of operations
to perform when exiting the state (cleanup, logging, etc.), `transitionToAction` is
the operation to perform when entering a state (initialization, music change, etc.),
and `startupAction` is what to perform when this state is the first state the game
starts up in.

<img src="/images/2017/Feb/FlowStates.png">

To clarify, `startupAction` is mostly for when debugging. For example: if I want
to start immediately in a gameplay scene instead of starting from the intro, this
will instantiate and set the UI to the correct state, initialize all of the scoring
variables, automatically pick a default car, and so on. This seems like an obvious
thing to do now, but in previous implementations, starting from an unconventional
state has necessitated hacks to make various systems work properly.

The state transitions for the game are defined in a Dictionary which maps a given
state to a StateTransition struct.

<img src="/images/2017/Feb/StateTransitions.png">

When a transition is invoked, if the next state is not valid based on the transition's
next states, the transition will fail. If it is valid, the "from" and "to" functions
will be invoked, and the new state will be set as the active state. Sometimes,
empty functions (`() => {}`) are passed as a transition's functions. This is done
when I don't actually need to load a new scene, or when no other operations need to
take place.
