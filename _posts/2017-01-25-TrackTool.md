---
layout: post
title: Track Tool
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

I made the track I've been using for testing by creating a path in Blonder, creating
an extrusion shape, extruding that along the path, and converting it to a mesh. I
thought that I might create some standard objects in Blonder to help try and establish
a pipeline for creating track segments, but I thought it would be more ideal to have
something that I could utilize right in Unity. By making a few tools for the engine,
I'd be able to edit tracks directly in scenes, have access to the spline and point
orientation data for any purpose, and I'd get to write editor scripts.

Fortunately, I saw a talk at Unite Boston two years ago that covered a large
chunk of this work: <a href="https://www.youtube.com/watch?v=o9RK6O2kOKo">A coder's guide to spline-based procedural geometry.</a>
It doesn't provide complete code, and some of the provided code needed some massaging
to function properly, but it helped me get the generation of a mesh based on an
extrusion shape and a spline working quickly.

After getting that in order, I started converting it and wrapping it with an editor
tool. So far, I can add/remove spline segments and edit their points and tangents. Doing
this updates the mesh and its MeshCollider in real time so that I can see how the changes
look, and also immediately test them with my car.

<img src="/images/2017/Jan/TrackTool.gif">

I can bake the segments down into a single track, or bake them into individual segments.
I'm not sure how much performance is going to be a concern at this point, but even
if large tracks work out nicely with respect to framerate, the idea of having reusable
smaller segments appeals to me too. The baked tracks are ScriptableObjects with their
curve information exposed. Presently I'm just using this to place road signs along
the edge of turns, but I'd like to use that information to blend mountains and other
scenery into the edge of the track.

More immediate next steps for this tool are to add better UV scaling which accounts
for curves, which the talk linked above goes into. The tool also doesn't handle
rotation of points and tangents on the segment curves which are going to be important.
Another near-future feature will be a visualization for how intense curves are,
so help me eyeball difficult segments without needing to drive the track.

<img src="/images/2017/Jan/CarOnGeneratedTrack.gif">
