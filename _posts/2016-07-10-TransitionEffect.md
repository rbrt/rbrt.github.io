---
layout: post
title: Transition Effect
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

Wow, it's been awhile since the last post! I hadn't worked on my transition
effect much over the last few months due to a pretty hectic period at work, but
last week I got things solved and managed to make a fairly general package
that can be dropped into any project. The end result is this:

<img src="images/2016/July/TransitionDemonstration.gif">

It's a transition between two test scenes that both occupy the same space in
world coordinates, have different geometry, have different ambient light, have
different UI canvases, and have different scene lights. Despite neither scene
being particularly interesting, the GIF above demonstrates how all of the
information contained in each scene is preserved and nothing is rendered twice.

To achieve this effect, there are two main components used. The first is a
SceneTransitionObject, or STO, and the second is the TransitionController.

Any scene that we want to transition to or from needs an STO, and right now it needs
to be the root of all objects in the scene. This isn't absolutely required, but
we would need to do an expensive FindObjectsOfType call instead of a
GetComponentsInChildren call if we didn't follow this guideline. An STO has
references to all of the lights, cameras, canvases, and renderers in a scene and
in Awake it will figure out if it is the current STO, or the next STO. In other
words, is it the *from* or *to* STO in the transition? All of an STO's cameras
are disabled and rendered manually every frame, which gives us total control
over what we're displaying.

The TransitionController has two RenderTextures (from and to) and a camera that
is ultimately responsible for rendering everything in the game. It can either be
rendering the contents of the "from" STO, the "to" STO, or some combination of
the two. When a transition is invoked, a special shader is used to smoothly
transition from the "from" texture to the "to" texture. To do this, the shader
needs to support two textures, and take an interpolation value.
The transition controller in the scene view looks like this:

<img src="images/2016/July/RenderingQuad.png">

A transition needs to be invoked when a new scene containing an STO is loaded
additively. The TransitionController will yield on the existence of a new STO,
and then it will use the following code to control individual rendering of each
scene once per frame:

<img src="images/2016/July/RenderTransitionFrameSample.png">

What is happening here is as follows: We disable all of the renderers and lights
in the new scene, and then we call the current scene's STO's RenderFrame method.
This will trigger a render to our "from" RenderTexture. Then we turn on all of
the renderers and lights in the new scene, disable all of the renderers and lights
in the current scene, and render the contents of the next scene to the "to" RenderTexture.
This continues until the transition is done, at which point we set the "to" STO to
be the current one (or, the "from" STO), unload the previous scene, and resume
rendering only the "from" STO's contents.

Using this technique, any shader that interpolates between textures can be inserted
and used to transition from gameplay to menu screens, gameplay to gameplay... or
whatever really. Here's an example of it in action to transition from a title screen
to gameplay in a side project I'm occasionally hacking on:

<img src="images/2016/July/GameTransition.gif">

I plan to make this available on the asset store or on GitHub or something
eventually. I just need to write up a bit of documentation and handle a few edge
cases.
