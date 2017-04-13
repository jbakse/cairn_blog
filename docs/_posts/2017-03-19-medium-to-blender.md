---
layout: post
title:  "Creating 3D Assets Part 1 : Modeling Workflow Using Oculus Medium and Blender"
date:   2017-04-12 12:00:00 -0500
categories: modeling 3d medium vr blender meshlab
author: Greg Schomburg
poster_image: /media/medium_workflow/meshlab_002.png
---

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_002.png">
	</figure>
</div>

I suck at modeling in blender

but I'm a pretty decent sculptor

did some initial level sketches with tiltbrush, but not ideal for actually creating geometry to work with

medium is a stupid name and difficult to search for on google



Using Oculus Medium on a HTC Vive with Revive. If you haven't tried it, try it it's worth it
Controler mapping takes a minute to get used to but it's great once you get it

tools you'll need: Meshlab, Mediumm, and Blender

## Modeling in Medium

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_001.png">
		<figcaption>
		Sculpting
		</figcaption>
	</figure>
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/medium_001.png">
		<figcaption>
		Cool
		</figcaption>
	</figure>
</div>
So first do some sculpting

Then save it, then export it as obj

Layers will work

Here's where it get exported to

## Cleaning up with Meshlab

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/medium_workflow/meshlab_004.png">
	</figure>
</div>

if you just bring it into blender you will see how gross it is
<img src="{{site.baseurl}}/media/medium_workflow/medium_blender_jackednormals.png">
Can also probably do all this stuff in Blender, but I know how to do it in Meshlab

Meshlab also has all sorts of tools for fixing gross geometry

Open it in Meshlab

Optimize it
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
fix the normals
export as an obj

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

bring it into blender
adjust smoothing to taste
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
move to correct position on the axis

create the UV maps

export as fbx for substance painter

next time talk about substance painter