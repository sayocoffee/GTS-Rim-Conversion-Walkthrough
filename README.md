# A *beginners'* Gran turismo sport rim conversion walkthrough
---

## Preface
This isn't meant to ba a definitive guide on Gran Turismo Sport rim conversion, its only suposed to serve as a documentation of the process for absolute beginners. I have relatively few experience in modding, so I might have made some mistakes along the way, if such is the case, please contact me and I will do my best to fix them. This is a learning process from me, any advice I can get, is advice i'm able to give back to the community.

## What is "rim swapping"?
Rim swapping is a process where you replace the existing rims on an existing car for a new set of rims. The old way of swapping rims involved manually swapping them in 3D software, but now there is a new method which uses a Custom Shaders Patch feature (elaborate) which makes the method more convenient and more respectful to the original car (if done in a tasteful fashion)

## Why is "rim swapping" frowned upon?
(elaborate, add pics of bad examples)

For the aformentioned reasons, I will not be covering the rim swapping process.

## Why convert rims from Gran Turismo Sport (GTS)?
Gran Turismo Sport is usually the game where you can obtain **accurate** and **high-poly** rims. Their models are also extracted in quads, meaning working with them will be much simpler. (I'll go more in depth further ahead) Generally, some textures are also very good, meaning you won't have to spend much time reworking them.

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


This guide will use 3ds max 2022 and Rizom 2020.1.

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







