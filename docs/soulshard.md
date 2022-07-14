---
layout: default
---

## Soul Shard
Soul Shard is a cooperative puzzle platformer that draws inspiration from EA's 'It Takes Two'. It is being developed by [19 Souls on Board](https://www.19soulsonboard.com/about), a team of 19 student developers from Cohort 18 at the Florida Interactive Entertainment Academy on the downtown campus of the University of Central Florida. I'm assisting the team as a technical artist this summer.
* The development update to the game can be viewed [here](https://www.youtube.com/watch?v=cN4vf7va254). 
* The repository containing my contributions to the project can be found [here](https://github.com/19SOB/ucf-fiea-19sob-capstone-project-temp).

<table border="0">
 <tr>
    <td><a href="../files/SoulShard.png" data-lightbox="soulShard" data-title="Soul Shard Poster"><img src="../files/SoulShard.png" style="width:100%"></a></td>
    <td><a href="../files/19SOB.png" data-lightbox="soulShard" data-title="19 Souls on Board Logo"><img src="../files/19SOB.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Soul Shard Poster</td>
    <td>19 Souls on Board Logo</td>
 </tr>
</table>

### 1.0 Smoke System
My first task was to design and develop a stylized explosive smoke particles for various machinery and explosions in the game. The basic idea was to develop a functional prototype and then refine it in the iterative design process.

### 1.1 Cloud Texture
Initially, I designed various cloud textures with separate RGB channels for Base Color, Emmisivity and Opacity Mask. <br><br>
<a href="../files/CloudRGB.png" data-lightbox="cloudrgb" data-title="RGB Cloud Texture"><img src="../files/CloudRGB.png" style="width:100%"></a>

### 1.2 Smoke Material
* The smoke material was made using these textures. 
* The emmisivity and particle colors were exposed for editing while making the particles. <br><br> 
<a href="../files/CloudMat.png" data-lightbox="smokemat" data-title="Smoke Material"><img src="../files/CloudMat.png" style="width:100%"></a>

### 1.3 Smoke Particles - 1st iteration
* The smoke particles were made using the Niagara VFX system. 
* The particles (100) were made to spawn in a burst around a cylinder with an initial velocity radially outwards. 
* A positive gravitational force was added to make the particles rise with a drag coefficient to smoothen things and make it feel natural. 
* Individual particles also received rotation in addition to a colour (the exposed parameter) that was lerped from grey to black .<br><br>
<a href="../files/Smoke1.gif" data-lightbox="smokepart1" data-title="Smoke Particles - 1st iteration"><img src="../files/Smoke1.gif" style="width:100%"></a>

### 1.4 Smoke Particles - 2nd iteration
* A light renderer was added to the particles to further intricately define the explosion.
* The light renderer was started off at the same initial position as the smoke particles.
* The intensity was lerped from 100 to 0.  <br><br>
<a href="../files/Smoke2.gif" data-lightbox="smokepart2" data-title="Smoke Particles - 2nd iteration"><img src="../files/Smoke2.gif" style="width:100%"></a>

### 1.5 Debris Texture
The debris texture was made in photoshop using online reference images and the brush tool. <br><br>
<a href="../files/DebrisTex.png" data-lightbox="debtex" data-title="Debris Texture"><img src="../files/DebrisTex.png" style="width:100%"></a>

### 1.6 Debris Material
The debris material was created using the debris texture in a similar fashion to the smoke material. <br><br>
<a href="../files/DebrisMat.png" data-lightbox="debmat" data-title="Debris Material"><img src="../files/DebrisMat.png" style="width:100%"></a>

### 1.7 Smoke Particles - 3rd iteration
* The debris particle was given the same parameters as the smoke particle.
* Since the debris appeared lighter, the drag was reduced and gravitational force (positive) was raised to increase the spread.
* Apart from that, a fountain emitter was assigned the same debris material to make the spread look more abrupt.  <br><br>
<a href="../files/Smoke3.gif" data-lightbox="smokepart3" data-title="Smoke Particles - 3rd iteration"><img src="../files/Smoke3.gif" style="width:100%"></a>

### 1.8 Spark Texture
The spark texture with separate RGB channels was obtained online. <br><br>
<a href="../files/Spark.png" data-lightbox="sparktex" data-title="Spark Texture"><img src="../files/Spark.png" style="width:100%"></a>

### 1.9 Spark Material
* The spark material was made using the spark texture. 
* The blue channel was used as the opacity mask.
* The emmisive color was obtained after combining red and yellow. <br><br>
<a href="../files/SparkMat.png" data-lightbox="sparkmat" data-title="Spark Material"><img src="../files/SparkMat.png" style="width:100%"></a>

### 1.10 Smoke Particles - Final iteration
* The spark particles were given the same parameter as the debris particle, i.e. a higher spread emitter and a fountain emitter.  <br><br>
<a href="../files/Smoke4.gif" data-lightbox="smokefin" data-title="Smoke Particles - Final iteration"><img src="../files/Smoke4.gif" style="width:100%"></a>

### 1.11 Other Variations
Few other variations of the smoke system <br>

<table border="0">
 <tr>
    <td><a href="../files/Smoke5.gif" data-lightbox="ov" data-title="Less stylized system"><img src="../files/Smoke5.gif" style="width:100%"></a></td>
    <td><a href="../files/Smoke6.gif" data-lightbox="ov" data-title="Debris only system"><img src="../files/Smoke6.gif" style="width:100%"></a></td>
    <td><a href="../files/Smoke7.gif" data-lightbox="ov" data-title="Puff system"><img src="../files/Smoke7.gif" style="width:100%"></a></td>  
 </tr>
 <tr>
    <td>Less stylized system</td>
    <td>Debris only system</td>
    <td>Puff system</td>
 </tr>
</table>
*Tap on the image to zoom*

### 2.0 Flame system
My subsequent task was to design & develop flame systems for different purposes like burning coal, chimneys, explosion, etc.

### 2.1 Noise Texture
A stylized noise texture was created to serve as the opacity mask for the flame material. <br><br>
<a href="../files/NoiseTex.png" data-lightbox="noisetex" data-title="Noise Texture"><img src="../files/NoiseTex.png" style="width:100%"></a>

### 2.2 Flame Material
* Parametrically controlled texture coordinate was masked to obtain a controllable gradient. The value is clamped between 0 and 1 to prevent excessive bleeding.
* The noise texture was added to give fire-like shape to the mask.
* The UV map of the texture was given a panner (with texture coordinate as input) to animate it, depicting a burning fire.
* A RadialGradientExponential (with texture coordinate as input) was subtracted from the mask to prevent square edges.
* The tiling, erosion & color of the material were exposed as dynamic parameters to be controlled by the Niagara system. <br><br>
<a href="../files/FlameMat.gif" data-lightbox="flamemat" data-title="Flame Material"><img src="../files/FlameMat.gif" style="width:100%"></a>

### 2.3 Flame Particles - 1st iteration
* Majorly, the structure of flame system was completed during the formation of material itself.
* The sprites were spawned in a circular grid with different rotations to give a 3D look.
* The color was lerped between yellow and red. <br><br>
<a href="../files/FlameVFX.gif" data-lightbox="fp1" data-title="Flame Particles - 1st iteration"><img src="../files/FlameVFX.gif" style="width:100%"></a>

### 2.4 Flame mesh
The flame system previously made was disapproved by the team for being too toony and not matching the game tone setting. So I decided to replace the sprite based particle system to a mesh one. I modeled an icoshpere mesh with decimate modifier for this purpose to provide randomness. <br><br>
<a href="../files/FlameMesh.png" data-lightbox="flamemesh" data-title="Flame mesh"><img src="../files/FlameMesh.png" style="width:100%"></a>

### 2.5 Flame material
The flame material was created simply by assigning the particle color input to the emmisive color of the material so that we can assign it later in the emmiter itself. <br><br>
<a href="../files/FlameMat.png" data-lightbox="flamat" data-title="Flame material"><img src="../files/FlameMat.png" style="width:100%"></a>

### 2.6 Flame Particles - Final iteration
* A fountain based emitter is used after removing gravity, cone velocity, drag and scaleColor just retaining the initial properties.
* The default sprite renderer is replaced with a mesh renderer and the icosphere and the flame material we created is assigned.
* The particles were assigned a random vertical velocity so that variance in the fire's peak giving it a natural eye.
* They're scaled down in size as they reach up to give an inverted conical shape by using bezier curves to keep the transition smooth.
* The color is lerped between yellow and red with the lifetime of the particle. <br><br>
<a href="../files/FlameVFX2.gif" data-lightbox="fpfin" data-title="Flame Particles - Final iteration"><img src="../files/FlameVFX2.gif" style="width:100%"></a>

### 3.0 Footprint System
Further I was assigned the task to develop a snow-based footprint system over snow for the main characters (Ambrose and Nimue).  

### 3.1 Footprint Sprites - 1st iteration
* I used a snow texture which I found online to make the footprint sprites.
* The foot impressions of the right foot of both the characters were traced using the pen tool and the texture was masked to make the footprint sprites.
* The left footprint sprite was simply made by inverting the image horizontally.

<table border="0">
 <tr>
    <td><a href="../files/AmbroseFI.png" data-lightbox="fi" data-title="Ambrose Foot Impression"><img src="../files/AmbroseFI.png" style="width:100%"></a></td>
    <td><a href="../files/NimueFI.png" data-lightbox="fi" data-title="Nimue Foot Impression"><img src="../files/NimueFI.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Ambrose Foot Impression</td>
    <td>Nimue Foot Impression</td>
 </tr>
</table>
*Foot Impressions*


<table border="0">
 <tr>
    <td><a href="../files/AmbroseFPS1.png" data-lightbox="fs" data-title="Ambrose Footprint Sprite"><img src="../files/AmbroseFPS1.png" style="width:100%"></a></td>
    <td><a href="../files/NimueFPS1.png" data-lightbox="fs" data-title="Nimue Footprint Sprite"><img src="../files/NimueFPS1.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Ambrose Footprint Sprite</td>
    <td>Nimue Footprint Sprite</td>
 </tr>
</table>
*Footprint Sprites*

### 3.2 Footprint Material - 1st iteration 
* The material used for the footprints was a deferred decal material with blending mode set to translucent so that you can apply it as a decal.
* The alpha of the texture/sprite was assigned to the opacity of the material and the RGB values to the base color. <br><br>
<a href="../files/FPMat1.png" data-lightbox="fm1" data-title="Footprint Material - 1st iteration"><img src="../files/FPMat1.png" style="width:100%"></a>

### 3.3 Footprint Blueprint
* An actor blueprint is created for both left and right footprints.
* A decal facing downwards with the footprint material is added as the child to the DefaultSceneRoot.
* The decal is made to fade away gradually after 5 seconds. <br><br>
<a href="../files/FPBP.png" data-lightbox="fpb" data-title="Footprint Blueprint"><img src="../files/FPBP.png" style="width:100%"></a>

### 3.4 Adding to the third person blueprint
* I used the default third person character provided by Unreal to playtest the footprints.
* In the TPC blueprint, planes are added as a child of the mesh and the respective foot as the parent socket so that it snaps perfectly with the foot's movement.
* The planes are rendered as invisible (hidden in game), events are prevented from overlapping, and collisions are disabled as they're just meant for spawn reference to the footprints. <br><br>
<a href="../files/TPBP.png" data-lightbox="addtpb" data-title="Third Person Blueprint"><img src="../files/TPBP.png" style="width:100%"></a>

### 3.5 Animation Notifier
* Animation notifiers are added for each footprint to spawn at the appropriate time in the running animation.
* In the third person animation blueprint's event graph, a character reference is set and cast to the third person character as the blueprint awakes.
* In the third person character blueprint's event graph, two new custom events are introduced to spawn the footprints.
* The event is meant to spawn an actor from the footprint class we created earlier. 
* The foot reference is assigned to the spawn location. 
* The actor rotation is assigned to the spawn rotation.
* The spawn scale was decided after playtesting.
* The custom events are assigned to the animation notifier in the third person animation blueprint's event graph.

<table border="0">
 <tr>
    <td><a href="../files/AnimNoti.gif" data-lightbox="tpb" data-title="Adding run animation notifier"><img src="../files/AnimNoti.gif" style="width:100%"></a></td>
    <td><a href="../files/TPAnimBP.png" data-lightbox="tpb" data-title="Third person animation event graph"><img src="../files/TPAnimBP.png" style="width:100%"></a></td>
    <td><a href="../files/TPCharBP.png" data-lightbox="tpb" data-title="Third person character event graph"><img src="../files/TPCharBP.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Adding run animation notifier</td>
    <td>Third person animation event graph</td>
    <td>Third person character event graph</td>
 </tr>
</table>
*Tap on the image to zoom*

### 3.6 1st Output
<a href="../files/FP1.gif" data-lightbox="op1" data-title="Footprint System"><img src="../files/FP1.gif" style="width:100%"></a>

### 3.7 Footprint Sprites - Final iteration
The team pinpointed that the current footprint lacked originality as snow footprints are generally a little darker (dark grey/blue) with blue tint on the edges. Apart from this, they suggested to add normal information to the footprints aswell.
* I decreased the exposure of the textures, added bluish tint on the edges using the brush (Chalk 2) tool.
* Further, I generated the normals using the inbuilt 3D tools provided in Photoshop. (which turned out to be one of my most laggy workflow experiences with Photoshop).

<table border="0">
 <tr>
    <td><a href="../files/AmbroseFPS2.png" data-lightbox="fp2" data-title="New Ambrose footprint texture"><img src="../files/AmbroseFPS2.png" style="width:100%"></a></td>
    <td><a href="../files/NimueFPS2.png" data-lightbox="fp2" data-title="New Nimue footprint texture"><img src="../files/NimueFPS2.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>New Ambrose footprint texture</td>
    <td>New Nimue footprint texture</td>
 </tr>
</table>
*Footprint Textures/Sprites*

<table border="0">
 <tr>
    <td><a href="../files/AmbroseFPN.png" data-lightbox="fn" data-title="Ambrose footprint normal"><img src="../files/AmbroseFPN.png" style="width:100%"></a></td>
    <td><a href="../files/NimueFPN.png" data-lightbox="fn" data-title="Nimue footprint normal"><img src="../files/NimueFPN.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Ambrose footprint normal</td>
    <td>Nimue footprint normal</td>
 </tr>
</table>
*Footprint Normals*

### 3.8 Footprint Material - Final iteration
The footprint material was modified to support normal information and the normal map textures generated were assigned. <br><br>
<a href="../files/FPMat2.png" data-lightbox="fmfin" data-title="Footprint Material - Final iteration"><img src="../files/FPMat2.png" style="width:100%"></a>

### 3.9 Final Output
<a href="../files/FP2.gif" data-lightbox="newfp" data-title="New footprint system"><img src="../files/FP2.gif" style="width:100%"></a>

### 4.0 Snowstorm System
My next task was to design and develop a snowstorm system for the yard area. I was provided with a [reference video](https://www.shutterstock.com/video/clip-1058627680-dense-heavy-blizzard-snowstorm-vfx-insert-slow-motion) for the same.

### 4.1 Snow Particles
* I found this task quite easy and felt that simply a fountain emitter with the default particle renderer would do the trick.
* So, I created a fountain emitter and inverted its initial velocity to make the particles fall downwards instead of upwards. 
* The particles were made to spawn around a big sphere.
* The trajectory cone's apex angle was increased as well to increase the spread of the particles.
* The gravity was decreased and drag was increased to make the snowfall appear more genuine. <br><br>
<a href="../files/Snow1.gif" data-lightbox="sp" data-title="Snow Particles"><img src="../files/Snow1.gif" style="width:100%"></a>

### 4.2 Wind Material
As I had anticipated, I was suggested to add more depth to the snowstorm. The idea was to make the snow more dramatic by introducing a wind system. They provided a [reference video](https://www.youtube.com/watch?v=sGkh1W5cbH4) aswell.
* A translucent unlit material was chosen for the wind particles.
* The emissive color was made to be driven by the particle color. 
* The opacity was controlled by the multiplication of the alpha value of the particle with a RadialGradientExponential to introduce a smooth gradient fall-off that would make the wind look natural. <br><br>
<a href="../files/WindMat.png" data-lightbox="windmat" data-title="Wind Material"><img src="../files/WindMat.png" style="width:100%"></a>

### 4.3 Wind Particles
* A new Cascade particle system is created and the rendering for the default emitter is turned off.
* The particle is given random horizontal velocity with minor deviations in other directions.
* An emitter for trails is added and it's made to follow the first emitter and spawn alongside it.
* The wind material created earlier is added to the trail emitter.
* The scale is made to represent a long trail.
* The direction of velocity is made to ribbon over its lifetime to make the trail follow a wave-like pattern.
* The particles are made to spawn around a sphere with controllable radius to contol the spread. <br><br>
<a href="../files/WindPart.gif" data-lightbox="wpart" data-title="Wind Particles"><img src="../files/WindPart.gif" style="width:100%"></a>

### 4.4 Fog Texture
* A smooth noise texture (obtained online) was used as the fog texture for smooth light absorption (extinction). <br><br>
<a href="../files/FogTex.png" data-lightbox="fogtex" data-title="Fog Texture"><img src="../files/FogTex.png" style="width:100%"></a>

### 4.5 Fog Material
* A volume-based material with additive blending is created for the fog to be volumetric.
* A sphere mask between world and particle position with particle radius as the mask's radius is used to control the rate of light absorption (extinction) of the material.
* The mask is parametrically controlled by a hardness and extinction value multiplied by RGB value of the texture I obtained earlier.
* The albedo of the material takes in the mutiplication of the sphere mask and the blend overlay between our texture and a RGB value parameter which we can control in the instance of that material.
* Thus we can control the hardness, light absorption rate and the color of the fog. <br><br>
<a href="../files/FogMat.png" data-lightbox="fogmat" data-title="Fog Material"><img src="../files/FogMat.png" style="width:100%"></a>

### 4.6 Fog Particle
* A new Cascade particle system is created and an instance of the fog material is assigned to it. 
* The particle is scaled only along the X-axis & Z-axis to represent a flat surface and its velocity is set to zero.
* This particle needs to be paired with an exponential height fog (with volumetric fog enabled) to render over the screen.
* The particles are spawned around a cylinder (having zero thickness) with its flat edge in the X-Z plane.

<table border="0">
 <tr>
    <td><a href="../files/FogEH.gif" data-lightbox="fogpart" data-title="Fog Extinction & Hardness"><img src="../files/FogEH.gif" style="width:100%"></a></td>
    <td><a href="../files/FogCol.gif" data-lightbox="fogpart" data-title="Fog Color"><img src="../files/FogCol.gif" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Fog Extinction & Hardness</td>
    <td>Fog Color</td>
 </tr>
</table>

### 4.7 Final Output
Finally the snow niagara system, wind cascade system, fog cascade system & an exponential height fog (with volumetric fog enabled) are added into a single blueprint actor to be used in the yard scene as a snowstorm system. <br><br>
<a href="../files/SnowStormFinal.gif" data-lightbox="ssys" data-title="Snowstorm System"><img src="../files/SnowStormFinal.gif" style="width:100%"></a>

### 5.0 Cable system
My next task was to come up with a physics-based cable system that was mostly to be used for cosmetic purposes in the game.

### 5.1 Cable Actors
Fortunately, Unreal comes preloaded with cable actors with rope physics for on-the-go usage. 
* These cables implement the traditional way for rope physics i.e. using a series of particles with motion constraints between them.
* The texture maps were obtained from the Quixel Megascans.
* The physics is constrained between objects that the cable is attached to them by using Physics constraint actor between the two objects.
* Cable's end is attached to any one of the objects. <br><br>
<a href="../files/Cable.gif" data-lightbox="cable" data-title="Cable System"><img src="../files/Cable.gif" style="width:100%"></a>

### 6.0 Glowing Crack Material
The team then assigned me the task to come up with materials with glowing cracks. They provided me with [references](https://assetstore.unity.com/packages/vfx/particles/spells/mesh-effects-67803#description) aswell. <br><br>
<a href="../files/gcrackref.png" data-lightbox="gcrack" data-title="Glowing Crack Reference"><img src="../files/gcrackref.png" style="width:100%"></a>

### 6.1 Crack textures
* As the reference for the material that I was provided with was a Unity asset, I tried reverse engineering the properties of the material to recreate it in Unreal.
* I could make out that a single color channel of the base map (Albedo) was inverted and clamped between 0 and 1 and was multiplied with the emissivity input for the material.
* The single channel input texture ensured that the light emitted took greyscale values according to the base map and we could control the intensity, rate, color tint, etc through the emissivity input.
* A normal map was also used to add depth information to the cracks to make them look more realistic.
* So I imported a non-uniform galvanized metal's texture maps (base & normal) from the Quixel Bridge for this purpose. 

<table border="0">
 <tr>
    <td><a href="../files/CrackBase.png" data-lightbox="crack" data-title="Base Map"><img src="../files/CrackBase.png" style="width:100%"></a></td>
    <td><a href="../files/CrackNormal.png" data-lightbox="crack" data-title="Normal Map"><img src="../files/CrackNormal.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Base Map</td>
    <td>Normal Map</td>
 </tr>
</table>

### 6.2 Emission Parameters
* The emissive color parameter of the material is governed by a time-dependent sine wave that leads to pulsating behavior by the glowing cracks.
* The sine input is given a **Rate** factor as its frequency, to control the rate of pulsation.
* Then the wave is given an offset governed by the **Pulse Intensity**. Its value is preferably kept to be greater than one to avoid negative waves (this prevents lag between the pulse cycles).
* The offseted wave function is amplified by a **Glow Intensity** factor to control the amplitude of the glow.
* Finally the entire amplified function is multiplied by an **Emissive Color** Vector parameter which governs the color of the glow.
* The **Rate, Pulse Intensity, Glow Intensity, Emissive Color** are parametrically exposed to be controlled by the instance of that material. <br><br>
<a href="../files/EmissionParameter.png" data-lightbox="empar" data-title="Emission Parameters"><img src="../files/EmissionParameter.png" style="width:100%"></a>

### 6.3 Emission Shape
* The base color of the material is governed by the base map of texture and a **Base Tint** Vector factor.
* The base map is blend overlayed with the **Base Tint** as the base. This ensures that whenever the blend is greater than half the grey value, it will get screened else it will get multiplied. (Every blend option was tried and the Overlay type was found to be best suited for our purpose).
* The final blend output is multiplied again with the base map and assigned to the base color of the material.
* The normal map is assigned as the material's normal as it is.
* The shape of the emission is governed by a single color channel of the base map (all three were tried and the Red channel felt the most appealing to the eyes).
* The color input is inverted using 1-x node and it is assigned a **Coverage** parameter as the exponent.
* The value is clamped between 0 and 1 and is multiplied by amplified function obtained above and finally assigned to the emissive color property of the material. 
* The **Base Tint & Coverage** are parametrically exposed to be controlled by the instance of that material. <br><br>

<a href="../files/EmissionShape.png" data-lightbox="emsh" data-title="Emission Shape "><img src="../files/EmissionShape.png" style="width:100%"></a>

### 6.4 Final Output
A material instance of this material was created and assigned to one of the items in the game.

<table border="0">
 <tr>
    <td><a href="../files/Coverage.gif" data-lightbox="parameters" data-title="Changing Coverage"><img src="../files/Coverage.gif" style="width:100%"></a></td>
    <td><a href="../files/GlowIntensity.gif" data-lightbox="parameters" data-title="Changing Glow Intensity"><img src="../files/GlowIntensity.gif" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Changing Coverage</td>
    <td>Changing Glow Intensity</td>
 </tr>
</table>

<table border="0">
 <tr>
    <td><a href="../files/PulseIntensity.gif" data-lightbox="parameters" data-title="Changing Pulse Intensity"><img src="../files/PulseIntensity.gif" style="width:100%"></a></td>
    <td><a href="../files/Rate.gif" data-lightbox="parameters" data-title="Changing Rate"><img src="../files/Rate.gif" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Changing Pulse Intensity</td>
    <td>Changing Rate</td>
 </tr>
</table>

<table border="0">
 <tr>
    <td><a href="../files/EmissiveColor.gif" data-lightbox="parameters" data-title="Changing Emissive Color"><img src="../files/EmissiveColor.gif" style="width:100%"></a></td>
    <td><a href="../files/BaseTint.gif" data-lightbox="parameters" data-title="Changing Base Tint"><img src="../files/BaseTint.gif" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Changing Emissive Color</td>
    <td>Changing Base Tint</td>
 </tr>
</table>
