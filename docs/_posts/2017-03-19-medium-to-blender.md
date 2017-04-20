---
layout: post
title:  "Oculus Medium to Blender Workflow"
date:   2017-04-12 12:00:00 -0500
categories: modeling 3d medium vr blender meshlab
author: Greg Schomburg
poster_image: /media/medium_workflow/meshlab_001.jpg
---

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_001.jpg">
	</figure>
</div>

I'm learning how to 3D model in Blender. I'm still really slow and I haven't trained my brain to properly approach box modeling. Physically sculpting however, comes pretty naturally for me. If I didn't have a phobia of dirty hands, I would probably do it a lot more. This is where VR swoops in and saves the day.

Modeling in VR is great; having the ability see and manipulate something at scale is very powerful. It's ideal for sketching out environments and then immediately experiencing them. There are quite a few different 3D drawing and modeling tools for VR, I have used [Oculus Medium](https://www.oculus.com/medium/) and [Google Tiltbrush](http://store.steampowered.com/app/327140/), but there are several other apps as well. [SculptrVR](http://store.steampowered.com/app/418520/) allows collaborative sculpting with low resolution voxels, [Quill](https://www.oculus.com/experiences/rift/1118609381580656/) is a vertex based VR drawing app and [MasterpieceVR](http://store.steampowered.com/app/504650/) is a free sculpting app that looks really promising. For this post I will be using Oculus Medium.

Medium is an Oculus exclusive. Which means if you have a Vive, you will need to install Oculus Home and Revive in order to purchase and run the app. I really didn't want to do either of those things, but I did and I do not regret it. It's a good app, super fun and really useful. The controller mapping takes a little time to get used to, particularly the mapping from joystick to touchpad. Overall though, the experience running Medium with the Vive has been solid.

Just a warning, using Medium on the Vive is not supported by Oculus, and there is always the potential that an update to the app will cause problems. For instance, last week a Medium update prevented me from launching the app until Revive updated to restore compatibility.
{:.alert}


## Sketching in VR

In our first sketches for Cairn, we actually used Tiltbrush to rough out our puzzle and level layouts. Tiltbrush is stroke based, it feels like drawing in 3D. This makes it fast and good for sketching, but the exported geometry is really only a series of ribbons that make up each stroke. This worked well for a reference to model around, but was not useable as final geometry. Medium, on the other hand, feels like sculpting and allows you to work with solid 3D shapes and brushes. Medium exports geometry as solid 3D meshes, but they still need some work before being ready to use in Blender or as a game asset. Let's get into it, here's what we will be working with: Oculus Medium, Meshlab, and Blender.


<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_002.jpg">
		<figcaption>
		Sculpting the whole head with symmetry.
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_003.jpg">
		<figcaption>
		Manually shattering the head with the cut tool. 
		</figcaption>
	</figure>
</div>



## Modeling in Medium


This is the fun part, sculpt some stuff. Here I'm sculpting the head of the owl-god which is controlled by the VR player in Cairn. The owl-god is an ancient shattered statue that is held together magically. This is a pretty good example of some of the benefits of sculpting with Medium. I sculpt the whole head using symmetry. Then switch to the 'cut' tool and begin breaking up the head by hand. Blender does have tools for shattering geometry, but doing it by hand gives me much finer control and makes it easier for me to go and do some custom carving on the inside of the head. The cut tool also separates the cut pieces onto different layers which will come in handy later.

## Exporting your Model

[clean up]
Save your work and once it's saved, use the export tool. It will export a .obj into the Medium sculpts folder. Something like `Documents/Medium/sculpts/[user_name]/[save_name]`

<div class="left-inline">
	<div class="figures">
		<figure>
			<img  src="{{site.baseurl}}/media/medium_workflow/blender_normals.jpg">
			<figcaption>
				Non Normal Normals
			</figcaption>
		</figure>
	</div>
</div>

If you bring the raw export into blender, it won't look quite right.
[image of problem] This is because the normals on the mesh created by Medium are not normalized. We can use Meshlab to fix this.

Medium is a terrible name to google for. When Medium came out it wasn't easy to find documentation, however you can now get the manual on the Medium homepage and the forums are quite active.

<div class="floatbreak"></div>
## Cleaning up with Meshlab

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/meshlab_002.jpg">
		<figcaption>
		Before decimation 120000 verts
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/meshlab_003.jpg">
		<figcaption>
		After decimation 5000 verts
		</figcaption>
	</figure>
</div>

Now that we have our obj we need to clean it up a bit. For that we will use Meshlab. Blender has similar features, but Meshlab gives us a few different options when we decimate. Meshlab has many other tools that you might find useful for cleaning up you meshes.

All that voxel modeling lead to some really complex geometry. Our first step will be to simplify it using the [blah blah] tool

[menu + options]
{:.step}

<div class="left-inline">
	<div class="figures small">
		<figure>
			<img src="{{site.baseurl}}/media/medium_workflow/meshlab_decimate.png">
		</figure>
	</div>
</div>

[a few things about the steps]

Our art style for Cairn is low-poly so we can crank up the simplification.  I reduced the number of vertices by 97%. That makes our model pretty chunky, but we'll be able to smooth that out later. Decimate however much you need.




The other thing we need to do is fix the vertex normals. It's also an easy fix using the [blah blah] tool.

<div class="floatbreak"></div>
[menu]
[Filters/Normals, Curvatures, and Orientation/Normalize Vertex Normals] Normalize Face Normals
There's no confirmation or dialog and you won't notice any difference in Meshlab, but the normalization worked.
{:.step}

Then we're good to go, export your mesh as an `.obj` and we can move on Blender.

## Finishing touches in Blender

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_002.jpg">
		<figcaption>
		Flat Shading
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_001.jpg">
		<figcaption>
		Smooth Shading
		</figcaption>
	</figure>
</div>

Import your `.obj` into Blender. I usually start by positioning centering my mesh and rotating into position.
[our style mixes flat and smooth shading in a particular way "curved low-poly" by smoothly connecting some polygons]
Now that it's nicely lined up we can play around with the vertex shading. We could just set it to flat shading, which looks pretty good for our ancient stone, but I still want a few smooth edges.

[Medium does something, we need to clear that to blah blah.] We can get this with auto smoothing, but first we need to clear some of the meshes smoothing data.

[steps]
[Shading:Smooth  -- Data Tab -- Auto Smoothing: on -- Clear Custom Split Normals Data -- Adjust Angle]
{:.step}

<div class="left-inline">
	<div class="figures">
		<figure>
			<img src="{{site.baseurl}}/media/medium_workflow/blender_clearcustom.png">
		</figure>
	</div>
</div>

Adjust smoothing to taste.

<div class="floatbreak"></div>
<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_003.jpg">
		<figcaption>
		Auto Smoothing
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_004.jpg">
		<figcaption>
		Auto Smooothing
		</figcaption>
	</figure>
</div>


End tease Substance