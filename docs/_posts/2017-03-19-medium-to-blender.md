---
layout: post
title:  "Creating 3D Assets Part 1 : Modeling Workflow Using Oculus Medium and Blender"
date:   2017-04-12 12:00:00 -0500
categories: modeling 3d medium vr blender meshlab
author: Greg Schomburg
poster_image: /media/medium_workflow/medium_001.jpg
---

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_001.jpg">
	</figure>
</div>

I'm learning how to 3D model in Blender. I'm still really slow and I haven't trained my brain to properly approach box modeling. Physically sculpting however, comes pretty naturally for me. If I didn't have a phobia of dirty hands I would probably do it a lot more. This is where VR swoops in and saves the day.

Modeling in VR is great; having the ability see and manipulate something at scale is very powerful. It's ideal for sketching out environments and then experiencing them. There are quite a few different 3D drawing and modeling tools for VR, I have used [Oculus Medium](https://www.oculus.com/medium/) and [Google Tiltbrush](http://store.steampowered.com/app/327140/), but there are several other apps as well. [SculptrVR](http://store.steampowered.com/app/418520/) allows collaborative sculpting with low resolution voxels, [Quill](https://www.oculus.com/experiences/rift/1118609381580656/) is a vertex based VR drawing app and [MasterpieceVR](http://store.steampowered.com/app/504650/) is a free sculpting app that looks really promising. For this post I will be using Oculus Medium.

Let me start by saying Medium is a terrible name to try and google for. When Medium came out it wasn't easy to find documentation, however you can now get the manual on the Medium homepage and the forums also are quite active. Secondly, Medium is an Oculus exclusive. Which means if you have a Vive, you will need to install Oculus Home and install Revive in order to purchase and run the app. I really didn't want to do either of those things, but I did and I do not regret it. It's a good app, super fun and really useful. Also if you have a Vive, the controller mapping takes a little time to get used to, particularly the mapping from joystick to touchpad.

And last note, if you do have a Vive there is always the potential to have Oculus update the app and cause Medium to no longer work. For instance right now  [2017/04/14] I can't get Medium to launch because of an update.
{:.alert}

In our first level sketches we actually used Tiltbrush to rough out our puzzle and level layouts. Tiltbrush's modeling is all vertex or stroke based, this makes it fast and good for sketching, but the exported geometry is really only a series of vertex ribbons that make up each stroke. This is good for reference to model around but not useable as final geometry. Medium, on the other hand, is high res voxels and allows you to work with solid 3D shapes and brushes. This gets us some decent geometry, but it still needs some adjustments before being ready to use as a game asset. Let's get into it, here's what we will be working with: Oculus Medium, Meshlab, and Blender.

## Modeling in Medium

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_002.jpg">
		<figcaption>
		Sculpting
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_003.jpg">
		<figcaption>
		Cool
		</figcaption>
	</figure>
</div>
This is the fun part, sculpt some stuff. Here I'm sculpting the head of the VR player the owl god (Sally). Sally is the remains of an ancient shattered statue that is held together magically. This is a pretty good example of some of the benefits of sculpting with Medium. I sculpt the whole head using symmetry. Then switch to the 'cut' tool and begin breaking up the head by hand. Blender does have tools for shattering geometry, but doing it by hand gives me much finer control and makes it easier for me to go and do some custom carving on the inside of the head. The cut tool also separates the cut pieces onto different layers which will come in handy later. If you want to learn more about Medium be sure to check out the manual or the forums.

Save your work and once it's saved, use the export tool. It will export a .obj into the Medium sculpts folder. Something like Documents/Medium/sculpts/[user_name]/[save_name]

## Cleaning up with Meshlab

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/meshlab_004.png">
	</figure>
</div>

Now that we have our obj we need to clean it up a bit. For that we will use Meshlab. Blender has similar features, but Meshlab gives us a few different options when we decimate. Meshlab has many other tools that you might find useful for cleaning up you meshes.

All that voxel modeling lead to some really complex geometry. Our first step will be to simplify it.
[menu + options]
Our art style for Cairn is lower poly and Sally is supposed to be an ancient shattered stone statue so we can crank up the simplification.  I reduced the number of vertices by 97%. That makes our model pretty chunky, but we'll be able to smooth that out later. Decimate however much you need.

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/meshlab_002.png">
		<figcaption>
		Before decimation
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/meshlab_003.png">
		<figcaption>
		After decimation
		</figcaption>
	</figure>
</div>
The other thing we need to do is fix the vertex normals. The Medium export has weird normals, you can see this if you open it up in Blender. It's also an easy fix.
<img src="{{site.baseurl}}/media/medium_workflow/medium_blender_jackednormals.png">
[menu]
[Filters/Normals, Curvatures, and Orientation/Normalize Face Normals & Normalize Vertex Normals]
There's no confirmation or dialog and you won't notice any difference in Meshlab, but the normalization worked. Then we're good to go, export your mesh as an obj and we're good to head on to Blender.

## Finishing touches in Blender

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_001.png">
		<figcaption>
		Shading Flat
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_002.png">
		<figcaption>
		Shading Smooth
		</figcaption>
	</figure>
</div>

Importing your obj into Blender. I usually start by positioning centering my mesh and rotating into position. Now that it's nicely lined up we can play around with the vertex shading. We could just set it to flat shading, which looks pretty good for our ancient stone, but I still want a few smooth edges. We can get this with auto smoothing, but first we need to clear some of the meshes smoothing data.

[steps]
[Shading:Smooth  -- Data Tab -- Auto Smoothing: on -- Clear Custom Split Normals Data -- Adjust Angle]

Adjust smoothing to taste.

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_004.png">
		<figcaption>
		Auto Shading
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_003.png">
		<figcaption>
		Auto Shading
		</figcaption>
	</figure>
</div>

Our last two steps will be to get the model ready for Substance Painter. Assign materials your meshes and name them.
[steps]
And then project your UV maps. 
[steps]
And lastly export your model as an FBX
[settings]

In part 2 I'll show my Substance Painter workflow.
