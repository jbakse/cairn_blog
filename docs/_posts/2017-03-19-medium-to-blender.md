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


## Modeling in Medium
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

This is the fun part, sculpt some stuff. Here I'm sculpting the head of the owl-god which is controlled by the VR player in Cairn. The owl-god is an ancient shattered statue that is held together magically. This is a pretty good example of some of the benefits of sculpting with Medium. I sculpt the half the head with mirroring turned on. Then use the 'cut' tool and begin breaking up the head by hand. Blender does have tools for shattering geometry, but doing it by hand gives me much finer control and makes it easier for me to go and do some custom carving on the inside of the head. The cut tool also separates the cut pieces onto different layers which can come in handy later.

## Exporting your Model

When you export from Medium, it will save an `.obj` file next to your saved sculpt. You can find all of your sculpts here: `Documents/Medium/sculpts/[user_name]/[save_name]`

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

If you bring the raw export directly into Blender, you will notice there is something wrong with the normals. The mesh normals exported from Medium are not normalized. We can use Meshlab to fix this. It is actually a simple fix, but it took some trial and error to figure out.

This is because Medium is a terrible name to google for. Not only is there the blogging platform, but there is also the hit CBS television show and about 2 billion  other things according to Google. Things have improved since Medium came out, but I've found the best place to find good information has been on the [Medium forums](https://forums.oculus.com/community/categories/medium).

<div class="floatbreak"></div>
## Cleaning up with Meshlab

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/meshlab_002.jpg">
		<figcaption>
		Before decimation 120000 faces
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/meshlab_003.jpg">
		<figcaption>
		After decimation 5000 faces
		</figcaption>
	</figure>
</div>

Now that we have our exported mesh we need to clean it up a bit. For that we will use Meshlab. Blender also has some decimate modifiers, but Meshlab gives us a few more options. Meshlab also has many other tools that are useful for cleaning up you meshes, like patching holes and repairing geometry.

All that voxel modeling lead to some really complex geometry. Our first step will be to simplify it using decimation.

Run `Quadric Edge Collapse Decimation` : Filters/Remeshing, Simplification and Reconstruction/Quadric Edge Collapse Decimation
{:.step}

<div class="left-inline">
	<div class="figures small">
		<figure>
			<img src="{{site.baseurl}}/media/medium_workflow/meshlab_decimate.png">
		</figure>
	</div>
</div>

There are a few different options when decimating. I typically stick to the dafaults and reduce the target number of faces. In the case of this mesh I can do some selections and run decimations on indiviual shattered pieces. This allows me to keep more detail in the face while greatly reducing the geometry for the smaller shards. Our art style for Cairn is low-poly so we can do some extreme decimation. I reduced the number of faces by 97%. That makes our model pretty chunky, but we'll smooth that out later in Blender. Decimate however much you need.

<div class="floatbreak"></div>
The other thing we need to do is fix those normals. It's also an easy fix using the Normalize Vertex Normals filter.

Run `Normalize Vertex Normals` : Filters/Normals, Curvatures, and Orientation/ Normalize Vertex Normals. There is no confirmation or dialog and you won't notice any difference in Meshlab, but the normalization worked.
{:.step}

Then we're good to go, export your mesh as an `.obj` and move on to Blender.

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

Import your `.obj` into Blender. By default the mesh will probably have it's shading set to `Smooth`. In our case that is not what we want, but just switching to `Flat` shading isn't right either. We want a mix. Some of our style references for Cairn were paparcraft sculptures that had a mix of curves and hard corners. Most of the edges and tight corners should be sharp and other edges can be smoothed out. Luckily this is exactly what the Auto Smooth setting does.

To enable `Auto Smooth` we first need to `Clear Custom Split Normals Data`. Select your mesh and both can be found in the `Data` tab. Once the custom data is the cleared the `Angle` field under Auto Smooth will become editable. Be sure that the meshes shading is also set to `Smooth` in the Tools tray.
{:.step}

<div class="left-inline">
	<div class="figures">
		<figure>
			<img src="{{site.baseurl}}/media/medium_workflow/blender_clearcustom.png">
		</figure>
	</div>
</div>

Something worth noting: clearing the custom split normal data will also actually fix our problem with normalizing the normals. So if you forget to do it in Meshlab you can still fix that here.

Adjust the smoothing angle to taste. This is the process we're using for most of the organic elements of Cairn like the rock platforms and trees. Auto Smooth is a quick way to get us close to the style that we're looking for, but it's not perfect and some of our assets will need a more manual approach. For instance the remaining architectural elements will likely be box modeled directly in Blender.

<div class="floatbreak"></div>
<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_003.jpg">
		<figcaption>
		Finding the right balance
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/blender_004.jpg">
		<figcaption>
		Smoothing the back
		</figcaption>
	</figure>
</div>

For my next post I will show off some of the next steps of our asset process: texturing in Substance Painter.