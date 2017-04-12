---
layout: post
title:  "Creating the Barrier Effect"
date:   2017-03-04 12:00:00 -0500
categories: shaders effects
author: Justin Bakse
poster_image: /media/barrier_effect/full_effect.png
---

One of the most prominent effects in *Cairn* is the large magical barrier. The Owl-God is trapped inside the barrier, but the Mouse can get out through small openings. To build the barrier effect we used a custom shader and a projector. The custom shader draws the surface of the barrier itself and a rim-light effect. The projector draws a bright line and a glow on objects that intersect the barrier.


<div class="figures">
	<figure>
		<video src="{{site.baseurl}}/media/barrier_effect/full_effect.mp4" controls></video>
	</figure>
	
</div>

## Creating the Plasma Effect


The plasma is created by combining two noise textures with the `min()` function in a custom shader. The result is similar to the darken blend mode in Photoshop.

<div class="figures">
	<figure>
		<img src="{{site.baseurl}}/media/barrier_effect/composite_min.png">
		<figcaption>
		Two textures (left, middle) are combined with min() (right).
		</figcaption>
	</figure>
</div>


This effect is animated by scrolling the two noise textures in different directions and speeds. To get a scrolling texture effect we need to change where we sample the textures over time. Unity's [built-in shader values](https://docs.unity3d.com/462/Documentation/Manual/SL-BuiltinValues.html) include the `_Time` variable. We scale `_Texture1Speed` and `_Texture2Speed` by this value to find the current scroll offset. Adding this offset to the mesh uvs when we sample the textures gives us the scrolling-texture effect.

```glsl
// sample the base textures
float2 t1 = _Time.y * _Texture1Speed;
float2 t2 = _Time.y * _Texture2Speed;
fixed4 tex1 = tex2D(_Texture1, i.uv1 + t1);
fixed4 tex2 = tex2D(_Texture2, i.uv2 + t2);
```

We combine the texture colors using `min()`, adjust the contrast of the effect using `pow()` and multiply the result with `_TextureColor` to tint the effect. `_TextureContribution` controls the overall plasma visibility.

```glsl
// combine/blend them
color_out.rgb = min(tex1, tex2);

// adjust contrast, intensity, and color
color_out.rgb = pow(color_out.rgb, _TexturePower);
color_out.rgb *= _TextureContribution * _TextureColor;
```

## Adding the Rim-Light

The second part of the shader is the rim-light effect. This effect adds a color glow to parts of the barrier seen from a sharp angle.

<div class="figures">
<figure>
	<img src="{{site.baseurl}}/media/barrier_effect/rim_off.png">
	<figcaption>Barrier effect without rim-light</figcaption>
</figure>
<figure>
	<img src="{{site.baseurl}}/media/barrier_effect/full_effect.png">
	<figcaption>Barrier effect with rim-light</figcaption>
</figure>
</div>

To build this effect we need to know two things: the vector from our eye to the fragment and the fragment's normal. We calculate this in the our vertex shader with help from Unity's built-in shader helpers.

```glsl
#include "UnityCG.cginc"
...
o.normal = UnityObjectToWorldNormal(v.normal);
o.viewDir = normalize(UnityWorldSpaceViewDir(mul(unity_ObjectToWorld, v.vertex)));
```


`UnityObjectToWorldNormal`, `UnityWorldSpaceViewDir`, `unity_ObjectToWorld` don't appear to be included in the docs, but they do appear in some of the official Unity example shaders and should be safe to use.
{:.alert}

In the fragment shader we can take the dot product of these vectors to find the edges: `dot(i.normal, normalize(i.viewDir))`. The dot product of two vectors is 0 when the vectors are perpendicular, which is the case at the very rim. Since we want the rim effect to be strongest on the edges, we invert the dot product by subtracting it from 1. We can then adjust the effect contrast with `pow()`, tint it with the `_RimColor` and `_RimContribution` params, and add it in.

```glsl
float rim = 1 - abs(dot(i.normal, normalize(i.viewDir)));
rim = pow(rim, _RimPower);
color_out.rgb += rim * _RimColor * _RimContribution;
```

## Using a Projector to Highlight Intersections

We use a [Unity Projector](https://docs.unity3d.com/Manual/class-Projector.html) to create the bright line where geometry intersects the barrier. A unity projector is a lot like a real-world projector: it projects a lighted image into the scene. The default projector material wasn't as bright as we wanted, so we copied it and added the `[hdr]` tag to its `_Color` property. This single change allows us to crank the brightness past 11.

```c
Properties {
	[HDR]
	_Color ("Main Color", Color) = (1,1,1,1)
	_ShadowTex ("Cookie", 2D) = "" {}
	_FalloffTex ("FallOff", 2D) = "" {}
}
```


<div class="figures">
<figure>
	<img src="{{site.baseurl}}/media/barrier_effect/projector_off.png">
	<figcaption>Projector off</figcaption>
</figure>
<figure>
	<img src="{{site.baseurl}}/media/barrier_effect/projector_ldr.png">
	<figcaption>LDR projector</figcaption>
</figure>
<figure>
	<img src="{{site.baseurl}}/media/barrier_effect/full_effect.png">
	<figcaption>HDR projector</figcaption>
</figure>
</div>


### Related Links

[Makin' Stuff Look Good: Winston's Barrier](https://www.youtube.com/watch?v=C6lGEgcHbWc)
: This fantastic video tutorial describes how to build a similar barrier effect.
