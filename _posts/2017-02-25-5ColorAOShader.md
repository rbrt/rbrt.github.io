---
layout: post
title: Multiple Color AO Shader
---
{{ page.title }}
----------------
<h5>{{ page.date | date: "%B %-d %Y" }}</h5>

I have a shader for the majority of my art assets now. It lets me colour things
and apply baked Ambient Occlusion without using any textures. The areas to colour are
determined via vertex colours as mentioned in a previous post, and the colours for
each area are specified on a material like this:

<img src="/images/2017/Feb/VertexAOMaterial.png">

The shader works by subtracting a threshold value from each vertex colour, and using
the `ceil()` function to convert it to either 1 or 0. Each colour is lerped with
the previous colour from highest threshold value to lowest, so that the lowest corresponding
colour is applied, and anything lower is thrown away.

I also ran into a really annoying issue trying to bake my AO into vertex data
while still being able to use the vertex colours. The first approach I tried was
to bake the AO into the vertex colour's alpha channel. Unfortunately this wasn't
possible because Blonder is unable to do it, and extensions I found online didn't
work properly. I then tried baking the AO into a second set of vertex colours, but
due to a limitation in Unity, only the first set of vertex colours are available
in shaders.

The approach I wound up using it to bake the AO into the model's UVs. Since I'm
not using textures (and don't want to), this seems to work well enough. I've considered
writing a postprocessor in Unity to write lightmap data to a mesh's vertex colour alpha,
but that seems like it might be worse to manage.

The relevant shader source to make all of this work is here:

<img src="/images/2017/Feb/VertexAOShader.png">

Using that I can paint a model's faces with varying degrees of black from a saved
palette:

<img src="/images/2017/Feb/VertexColors.png">

Then, auto-unwrap the model and do a lightmap pack to generate AO:

<img src="/images/2017/Feb/VertexColors.png">

Then, swap the UVs with the vertex colours:

<img src="/images/2017/Feb/UVs.png">

Then, bake the AO to the vertex colours (which are UVs right now so they're overwritten):

<img src="/images/2017/Feb/VertexAO.png">

Then I can switch the AO back with the original colour data, bring it into Unity,
and apply the shader to get this result:

<img src="/images/2017/Feb/InteriorInUnity.png">

Now if only I was better at making 3D art...
