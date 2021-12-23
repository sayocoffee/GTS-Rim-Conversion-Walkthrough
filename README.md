# A *beginners'* Gran turismo sport rim conversion walkthrough
---

## Preface
This isn't meant to be a definitive guide on Gran Turismo Sport rim conversion, its only suposed to serve as a documentation of the process for absolute beginners. I have relatively little experience in modding, so there is the potential for mistakes. If that is the case, please contact me and I will do my best to fix them. This is a learning process for me, any advice I recieve, is advice i'm willing and able to give back to the community.

## What is "rim swapping"?
Rim swapping is a process where you replace the existing rims on an existing car with a different set of rims. The older methodology involved manually swapping them in 3D software, but now there is a new method which uses a Custom Shaders Patch feature called Object Replacement which makes the method more convenient and more respectful to the original modder as you do not need the 3d files of the car. (of course, only if done in a tasteful fashion)

## Why is "rim swapping" frowned upon?
Rim swapping can be frowned upon as it often changes the original image, style or intent of a modders work. Therefore it has the capacity to make a modder's work appear differently to an audience which can sway their opinion about a modder. There is also the issue of permissions to edit a modders work. Rim swapping is a grey area with obtaining permission. The process is quite easy, and does not require the car's 3d files so often people do not feel the need to obtain permission.

For the aforementioned reasons, I will not be covering the rim swapping process.

## Why convert rims from Gran Turismo Sport (GTS)?
Gran Turismo Sport is more often than not the game where you can obtain **accurate** and **high-poly** rim 3d. Their models are also extracted in quads, this makes uv mapping easier and you can more easily edit them if they are innacurate, etc... (I'll go more in depth further ahead) Generally, some textures are also very good, meaning you won't have to spend much time reworking them.

Besides these practical terms, GTS rim conversion has a simillar methodology to GTS car conversion, meaning this is a good stepping stone for beginner modders looking to gain some experience before starting a big project.


## A quick rundown of required/recommended stuff

+ Content Manager;
+ KS Editor;
+ 3d software of choice (Blender/3ds Max);
+ (Optional) UV unwrapping software (Rizom UV);
  + If you have rizom, you will need a bridge plugin, which can be found for free [here](https://www.rizom-lab.com/bridges/ "Rizom link")
+ (Optional) Ripped copy of GTS;
+ (Optional) GTS model extraction tool;
+ (Optional) Texture conversion script (Can be found in SRP pinned);


You're also going to need experience with your 3d software of choice: The bare minimum for a rim conversion is deleting extra objects/edges, apply modifiers, materialization of objects and uv unwrapping.


This guide will use 3ds max 2022 and Rizom Real Space 2020.1.

## (Optional) Ripping the models/textures

After picking the rim you want to rip, using [this video](https://www.youtube.com/watch?v=4aZOF9_DiRo "GTS Rim Video") as aid, refer to [this list](http://url.com "GTS Rim List") and take note of the filename corresponding to the model you intend to rip. In my case, a friend wanted RAYS TE37v's, which corresponds to the ID `HE048` 


After you get the ID, go into the following directory of your ripped GTS copy: `...\..\...\GTS\CARPARTS\HQ` and locate the file corresponding to the ID: 

![Image](https://files.catbox.moe/vlltv1.jpg "Rim in Directory")

Using a GTS extraction tool, drag the file into the tool .exe and copy the .obj and generated texture folder into a new folder. **This will be your work directory.** 

Now, if you try to open the converted textures, they will look like colored squares. This is because they are in dxt10 format. To fix this, you need to run the texture conversion script on the texture folder. Now the extracted textures are in a useable format.

## Importing the model/ first steps.

Firstly, import the .obj file in your 3d software. Make sure to follow the settings shown in the pipeline. 

**Scale factor must be set to 1.** If this isn't the case, the way to fix this issue (**IN 3DS MAX**) is to:

+ On the topmost toolbar, open the "Customize" menu;

![Image](https://files.catbox.moe/t8oxxx.jpg "Customize menu")

+ Select "System Units Setup"

![Image](https://files.catbox.moe/lrk4s7.jpg "System Units Setup");

+ Make "Display Unit Scale" sure is set to meters;

![Image](https://files.catbox.moe/f9vnik.jpg "Display Unit Scale") 

+ Open the "System Units Setup" sub-menu and make sure System Unit Scale is set to Meters and "Respect System Units in Files".

![Image](https://files.catbox.moe/nhawbp.jpg "System Units Setup sub-menu") 

If you followed everything correctly, you should have your rim model in the viewport.

![Image](https://files.catbox.moe/emzsd8.jpg "Rim in viewport").

Most GTS models have duplicate meshes that are used for LODs, meaning you're gonna have to manually check and delete meshes that are overlaying eachother.


Now, in order to perform certain 3d operations over the objects, you need to convert every mesh to "Editable Poly" 

![Image](https://files.catbox.moe/d43yqd.jpg "Editable Poly").

**IMPORTANT NOTE: Many car parts are using tesselation. These meshes are marked with "_T" in their name. Thats why they look like they are low detail. But actually those are highest quality meshes. (Quote taken from a certain forum)**

### What is this tesselation thing and why is it important?

Gran Turismo's engine tesselates (or in simpler terms, subdivides) "_T" meshes live in game, which allows them to have "dynamic LODs". This feature isn't present in Assetto Corsa, meaning you have to apply a smooth modifier to those meshes.  

Some meshes come unwelded, probably due to the way the extraction tool works (unwelded edges usually follow UV seams), so you will have to perform a weld operation on **all meshes**:

+ In vertex selection mode ("1" Key on your keyboard) select every vertice in the mesh `CTRL+A`

+ Select the weld operation in the "Edit Geometry" menu;

![Image](https://files.catbox.moe/wcm3yg.jpg "Weld Operation")

+ Weld every vertex in your mesh with a very low treshold. 

![Image](https://files.catbox.moe/nqmaib.jpg "Low threshold welding").


After welding, apply a MeshSmooth/TurboSmooth modifier to the object. **DO NOT COLLAPSE THE MODIFIER.** The modifier stack collapses on export, meaning you will have simpler geometry to work with.

After deleting the above mentioned meshes and performing the smooth operation, give the remaining ones clear names, that will later on correspond to the materials they will have. 

![Image](https://files.catbox.moe/nj2h3t.jpg "Rim after deleting duplicates and renaming meshes")


## Conversion Process

After you've finished the first steps you can optionally quad low poly meshes, so you can smooth them to gain more detail.

**DO NOT PERFORM A SMOOTH OPERATION ON TRIANGULATED MESHES**

### Why is "smoothing tris" a bad thing to do?

Smoothing triangulated meshes will create unworkable topology and horrible shading issues.

![Image](https://files.catbox.moe/yojaqf.PNG "Comparison of smoothing quads/tris")

Above is a simple cube with 2 smoothing iterations. The awful results of subdivided triangles (on the right) are very clear.


### How can I "quad" meshes?

Quadding meshes is a very tedious albeit necessary task. There are a few methods you can use, but the most fool-proof one is manually finding and deleting diagonal edges in the mesh, as shown in a simple example below.

![Image](https://files.catbox.moe/06iz2n.PNG "A quick visual guide on quadding") 

AC Modder Trawa goes more in depth about quadding/retopologizing models in the [following video](https://www.youtube.com/watch?v=Tg-TauMHpWs "Trawa retopo vid").

In my case, I had found a triangulated mesh I wanted to smooth. 

![Image](https://files.catbox.moe/l0lqlf.jpg "Mesh to quad")

After quadding and smoothing:

![Image](https://files.catbox.moe/th6eqv.jpg "Quadded + smoothed mesh")


After I was finished with the whole process, it's time to assign materials.

## Materialization

Materials define the properties of a certain mesh. Things like leather, metal, plastic are some prime examples of materials being used in AC cars.

### Setting up the Material Editor (3DS MAX)

Press the 'M' key on your keyboard to open the Material Editor. You will see a menu with big spheres, which are samples for the materials you might be working with in your project. In order to see more of them simultaneously, open the `Options` menu and select the `Cycle 3X2, 5X3, 6X4 Sample Slots` 3 times.

![Image](https://files.catbox.moe/urp6zo.jpg "Increasing sample visibility")

## Basic Material Editor Functions

![Image](https://files.catbox.moe/xzc1cv.jpg "Material Editor Toolbar")

This is the Material Editor toolbar. I recommend you get accustomed to it since this will be used frequently for modding purposes. The main functions that are going to be used are the ones highlighted in the picture above. We're going to be covering them from left to right, top to bottom.

1. Get Material - Used to grab a material from a scene, to reapply onto another mesh.
2. Assign Material to Selection - Assigns a selected material onto a selected mesh.
3. Reset Map/Mtl (Material) to Default Settings - Deletes the selected material from the material editor.
4. Pick Material from Object - Acts as the generic Color Picker but for Materials.
5. Material Bar - Displays the current material's name. It's also where they're renamed.

### General Materialization Workflow

The general workflow for materialization is the following:

+ Attach all the meshes that will have the same material (eg. attach all plastic meshes)
+ Open the material editor, and using the Material Bar, give it a name following clear naming conventions and explicitly stating the surface properties it will have (if a material will be metal, name it as such). 
+ Select the mesh that will have the material created and assign the material using the method described in (2).

After working on the model and materializing, the next step is UV-Mapping.

## UV Unwrapping

### What is a 'UV'?

>UVs are two-dimensional texture coordinates that correspond with the vertex information for your geometry. UVs are vital because they provide the link between a surface mesh and how an image texture gets applied onto that surface. (...) By default, most 3D applications will create an automatic UV layout when the mesh is originally created. However if you were to drop the texture (...) directly onto the 3D model, the chances are good that you would see very undesirable results. This occurs because during the modeling process, the UVs aren't usually taken into account and, as a result, the 2D image can't wrap around a 3D object the way you would expect to see. Once your model is complete, in order to properly texture your model, you need to begin the process of laying out the UVs (often referred to as UV mapping). **This basically is the process of creating a 2D representation of your 3D object.** Imagine your model unfolded and flattened out into a flat 2D image. Where would the natural seams occur? Where on the 3D model would the most detail be needed? (...)

-From Understanding UVs - Love Them or Hate Them, They're Essential to Know (https://www.pluralsight.com/blog/film-games/understanding-uvs-love-them-or-hate-them-theyre-essential-to-know)

For AC modding, a proper UV unwrap is crucial as it will be used for baking AO maps (short for Ambient Occlusion)


### Some generic principles for AC oriented UV Mapping

1. Avoid planar mapping, as it produces more often that not suboptimal results, and horrible seams. Peel mapping is the preffered alternative at the moment.
2. Do not rely on auto seams and auto pack. Auto Seaming will try it's best to produce a stretchless UV, but in doing so it will create a lot of visible seams on your model. Auto pack will not be able to efficiently manage all of the UV space, meaning some parts will be losing detail unecessarily. 
3. Piggybacking off of (2), make sure to efficiently use all of your UV space, in order to have every part of the UV be the most detailed as it can be.
4. Place seams on places that are not visible in your model. 


UV unwrapping isn't really an algorithmic process, meaning the best way to learn is to look at good mapping and try to follow the same techniques.

AC modder Azuane has some good videos on the process.

+ [Rim UV Mapping 1 (28/01/2020)](https://www.youtube.com/watch?v=m4LJWP5B5uY)
+ [Rim UV Mapping 2 (09/05/2020)](https://www.youtube.com/watch?v=2fToss6JZ7Q)
+ [Car UV Mapping 1 (30/05/2020)](https://www.youtube.com/watch?v=9xtN_ZOWpMY)
+ [Car UV Mapping 2 (03/06/2020)](https://www.youtube.com/watch?v=iCOhwoTTQEk)
+ [Car UV Mapping 3 (18/07/2020)](https://www.youtube.com/watch?v=CJFwjUnhAn0)
+ [Car UV Mapping 4 (04/08/2020)](https://www.youtube.com/watch?v=LePGemCBUW8)
+ [Car UV Mapping 5 (05/01/2021)](https://www.youtube.com/watch?v=ATZ0nJ0X6mY)
+ [Car UV Mapping 6 (21/01/2021)](https://www.youtube.com/watch?v=blYNWoKOS2g)

Below are some rim UV maps from good AC car mods.

![Image](https://files.catbox.moe/d5nmfq.jpg)

Axis' Porsche 930

![Image](https://files.catbox.moe/jbt0qw.jpg)

Trawa/Azu's FD3S Type-A

![Image](https://files.catbox.moe/jg9gkh.jpg)

Trawa's FD3S C-West

![Image](file:///C:/Users/Gustavo/Desktop/guide/pschd_rim_uv.jpg)

Psychedd's FD3S Re-Amemiya

![Image](https://files.catbox.moe/erisa4.jpg)

Psychedd's Integra DC2

Note how all of the UV's are following in one way or the other the principles i've listed above.

## Model Exporting and KS Editor Overview

By now your model should be ready to be exported.

Export your model using the recommended settings in the pipeline and load up the .fbx file in KS Editor (`...\assettocorsa\sdk\editor`).

### Some notes about ksEditor 
There are many tutorials that you can use to learn the basics and familiarise yourself with the software. I found [this video](https://www.youtube.com/watch?v=bT0uIbSrrr8&ab "Assetto Corsa ksEditor Introduction & Basics Tutorial") to be of most use.
Generally ksEditor is where you will be assigning shaders to your model, applying textures and exporting into Assetto Corsa through kn5 files.
