---
Title: DreadEngine
date: 2020-02-05 12:00:00
categories: [Portfolio, CPP]
---
## Dread Engine Mk1
In university, I got my first taste of computer graphics through a course focused on real-time rendering using [OpenGL](https://www.opengl.org/). We had to create two 3D objects with textures and add a couple of lights.

For my project, I used models made by other students and played around with [Phong Lighting](https://en.wikipedia.org/wiki/Phong_reflection_model) to light up the scene.

I also set up the camera so it could move around and explore everything.

[Github](https://github.com/ConnorY97/DreadEngine)

|Commit|Message|
|------|-------|
|[00](https://github.com/ConnorY97/DreadEngine/commit/7edda2e53a7e3459b78af3b92127d4d8c86585d0)|Initial commit|
|[01](https://github.com/ConnorY97/DreadEngine/commit/fc1e550ee4fd590651272a4681b309b8e1cfdc98)|Drawn to window using DreadEngine. Creating my own game engine|
|[02](https://github.com/ConnorY97/DreadEngine/commit/295690187bf4c9000f640595c120c7fd51d0bb4b)|Started work on shader. Currently not working|
|[03](https://github.com/ConnorY97/DreadEngine/commit/790f94dfbf66c28786840bf104cc66980bb59398)|Working Shader and IBO. Using Alex's shader class and Josh's IBO Code. Will need to rewrite to better understand|
|[04](https://github.com/ConnorY97/DreadEngine/commit/cf9c99e756a6c13f1be05c3b4b7ef13b5b6e9e35)|Auto stash before checking out "HEAD"|
|[05](https://github.com/ConnorY97/DreadEngine/commit/656993b71afa55205bcf917ed4c9311db748c075)|Working Engine. Lots of other peoples code that I'd like to rewrite.|
|[06](https://github.com/ConnorY97/DreadEngine/commit/310f26b820a9b9a898e9fa6f8035c5d2dc1989d7)|Working camera class. The camera can move around on the z and x axis but cannot rotate yet. BUT IT WORKS!|
|[07](https://github.com/ConnorY97/DreadEngine/commit/4cd39aff46dd156ab5dd4c78f6613261bcd1e3bc)|Fixes to the camera. Fixed some small issues with moving the camera and added rotation around the mouse. It is very janky but works|
|[08](https://github.com/ConnorY97/DreadEngine/commit/df85bcbfb7062fcf4aa654e870966fcf2a1b70df)|Writing my own cube. Made a cube using my own coordinates|
|[09](https://github.com/ConnorY97/DreadEngine/commit/c6f70b3537789ff4b8f770291e15502f445277a5)|Created the Mesh class. Completion of a simple mesh class and commenting done|
|[10](https://github.com/ConnorY97/DreadEngine/commit/98dce57764dc58f203229c22621a31911ce0154c)|Small changes to position. Slightly changed the position of the cube and the plane so that they rotate correctly|
|[11](https://github.com/ConnorY97/DreadEngine/commit/7fe63047a08ec48d85a0078da3312d99ecba82da)|Added Primitive shapes class. I can now make spheres, cubes and planes easily and I pretty sure that they actually work. To be proven wrong soon probably|
|[12](https://github.com/ConnorY97/DreadEngine/commit/f7cc18cb87024a3c6a72a2a530a890dc9e019054)|Fixed fly camera. Forward is no longer locked to world space but now is local to the camera which makes movement alot easier|
|[13](https://github.com/ConnorY97/DreadEngine/commit/b68c1f1bdb7465e5677693303068dfcd29f2ecbb)|Adding functionality. Adding some functionality to the game loop and some cleaning|
|[14](https://github.com/ConnorY97/DreadEngine/commit/b0ac3647463f0220b7e455e53075ee70a2ec9317)|OBJ Loader. Working OBJ loader and still functional program.|
|[15](https://github.com/ConnorY97/DreadEngine/commit/e741c1b9bcaf1b408f1630e5f369130f8d6d4af8)|Half working Texturing. Working texturing for one plane but now to get it working on a cube then other shapes|
|[16](https://github.com/ConnorY97/DreadEngine/commit/d8cb4425ca5f2176d9f2a67bbb1ac22f6bb447df)|WORKING TEXTURING. Got the goddamn texturing to work on a cube!! everything is facing the right way and is the right orientation!|
|[17](https://github.com/ConnorY97/DreadEngine/commit/612f09923cea0567d20d4fb37d4397037a48480e)|Working on lighting. The lighting is working but it is very messy and will need to be cleaned up alot!!|
|[18](https://github.com/ConnorY97/DreadEngine/commit/069d01fe9fb3ffb1475282121d40783f1f0959c3)|Working ambient shader. Fixed it so that it is a currently working ambient shader, to get the specular shader to work it requires a lot of work! So I will leave it for later.|
|[19](https://github.com/ConnorY97/DreadEngine/commit/22b33af7bfb6f9462921da40eea4abd6e323d1c4)|Working material lighting. I cant light an obj object with material lighting,. still need to get it working with textures|
|[20](https://github.com/ConnorY97/DreadEngine/commit/888ce78830923d5875cf8021b0c5ac4a45d7ea48)|Working separate light and texture shaders. I now need to get a texture to work with the light shader. But I have no idea how I am going to do that|
|[21](https://github.com/ConnorY97/DreadEngine/commit/735812368d629b83d693231d06fc6b46f5ee2c1d)|LIT TEXTURES. I had a 1 where I needed a 2 and of course that ruined everything.. Now cleaning everything and attempting to break thing into classes without breaking them|
|[22](https://github.com/ConnorY97/DreadEngine/commit/e24f1d07fb1462c13fa80a1769dc58cbd48068c5)|Started work on Object class + added models to git. Added the models as they were ignored for some reason. Also started work on the object class so I can move individual objects|
|[23](https://github.com/ConnorY97/DreadEngine/commit/c47472151c857e58356997cb49f694761a8d495e)|Currently working build. This build has two lights and models that can be moves, version control is a bit munted but fixing that now|
|[24](https://github.com/ConnorY97/DreadEngine/commit/55db12a29d2d66f32f9ad5857f600393444d3f64)|Fixed Merge Conflicts|
|[25](https://github.com/ConnorY97/DreadEngine/commit/18232eb5705e5d0d1a454bec6c724f755f40f387)|One lit and textured model. One super janky model that works but is super ugly!|
|[26](https://github.com/ConnorY97/DreadEngine/commit/c29a9916bc418ecd1a1fabf1e81ecf91a711bd56)|Fixed broken light. There was a problem with something honestly I don;t know but it works now so all there is left is to add the last object.|
|[27](https://github.com/ConnorY97/DreadEngine/commit/3ff6162f9bed7f848ee42279d9db9b9667d7ace7)|ITS DONE. There are two lit objects in the worlds worst game engine ever made but it is goddamn done!! Now I should make it better!|

#### Trailer
{% include embed/youtube.html id='kZRH7kmW67w' %}

## Dread Engine Mk2
My second shot at crafting a custom renderer I focused on tidying my code for better readability. It ended up with fewer features than the first one.

[Github](https://github.com/ConnorY97/DreadEngineMK2)

|Commit|Message|
|------|-------|
|[00](https://github.com/ConnorY97/DreadEngineMK2/commit/c4573b283b0ede75df8bebf0913e645beae2feb0)|Initial commit|
|[01](https://github.com/ConnorY97/DreadEngineMK2/commit/da322ba45c9985a355436260b71d1069a937604e)|Initial Commit. DreadEngineMK2 This is my second attempt at a game engine which I would like to make better than my first.|
|[02](https://github.com/ConnorY97/DreadEngineMK2/commit/0f95bcf7c6d0683ffd0dbeed987a496cf0ec1fe9)|Fixes. Fixes to the initial commit. Hopefully it will still work|
|[03](https://github.com/ConnorY97/DreadEngineMK2/commit/96812976565f42f34d7fb412ad03e7f9f87c98a6)|Adding ignore|
|[04](https://github.com/ConnorY97/DreadEngineMK2/commit/69cc548e4bfc19733e0a0d1bea38ea3d1853eeea)|Working on it|
|[05](https://github.com/ConnorY97/DreadEngineMK2/commit/d335984035ab9cefe8a768bc32b5fd7d4dc05cd9)|Render window. I have a render window opening displaying a colour and closing without any errors, good place to check point|
|[06](https://github.com/ConnorY97/DreadEngineMK2/commit/2a68c3fb1728df12327e5e8f04fb58f1179d1df7)|Application3D class created. Moved the creation of the window off the main, which helps with readability. I believe that it is still working|
|[07](https://github.com/ConnorY97/DreadEngineMK2/commit/68327d710a287e6d4285e9d99507586a6753ffc8)|THE FIRST TRIANGLE. Rendered the first triangle. The main has become very messy again so now the next thing to do it move the shaders into their own classes but in a way that actually works this time!. Things are progressing nicely and I understand what is going on|
|[08](https://github.com/ConnorY97/DreadEngineMK2/commit/68327d710a287e6d4285e9d99507586a6753ffc8)|Added shader class. Added in a stand alone shader class which at this point seems to work.. Going Well I hope|
|[09](https://github.com/ConnorY97/DreadEngineMK2/commit/4075990fc3bf8d6cad5e2be376e8a9b7732e79cb)|Textured Rectangle. Had an issue where the rectangle wasn't being drawn correctly but it was because I was using the wrong gldraw function. Make sure you use the right functions for the right situations|
|[10](https://github.com/ConnorY97/DreadEngineMK2/commit/d0cb8fff5b35b6e537d63e7f5f0298558192bfab)|Rectangle now has a smiley face. Added a second texture which is still able to be rendered onto the box|
|[11](https://github.com/ConnorY97/DreadEngineMK2/commit/ffd85702640806588dd3f5be433058ef9e60bf94)|Added transforms to vertex shader|
|[12](https://github.com/ConnorY97/DreadEngineMK2/commit/a4fd44d9824d5ba8243e5a87f095aa0a0d23eb2b)|Model matrix manipulation. Working on changing the model matrix which allows for moving objects around the scene.. Very cool.|
|[13](https://github.com/ConnorY97/DreadEngineMK2/commit/d2afc5541bbe7ad8338f5f8a0bbc0999754154eb)|Added camera. Added external camera class from last project.. Now all there is to do is clean up and then begin to try add physics|
|[14](https://github.com/ConnorY97/DreadEngineMK2/commit/ed6792c731358ad308e31dc71a4740b7c1a6ada5)|Adding gizmos. Adding external class gizmos|
|[15](https://github.com/ConnorY97/DreadEngineMK2/commit/79ff66a10b8b5c1e4b15a9289d9175e5ef1ef043)|Created Texture class and manager. and cleaned up the code a little bit|
|[16](https://github.com/ConnorY97/DreadEngineMK2/commit/deeb04b7d47168767d693a1f9c12f0c117dc647b)|Working texturemanager|
|[17](https://github.com/ConnorY97/DreadEngineMK2/commit/ac643d525cb74796fb599d1f84362560a891b413)|Code clean up|

## Dread Engine Mk3
Third attempt at a custom renderer with a specific purpose. My aim was to make a game using my own renderer with basic shape collisions. I was able to render 2 shapes in different colors then I stopped development on it.

[Github](https://github.com/ConnorY97/DreadEngineMk3)

|Commit|Message|
|------|-------|
|[00](https://github.com/ConnorY97/DreadEngineMk3/commit/d035a20b3ae8148b7b01e07a56856566427c2e2e)|Initial commit|
|[01](https://github.com/ConnorY97/DreadEngineMk3/commit/7900f38d9d970c729b3b9b01a4c8bb30a056f305)|Attempt no. 3 here we go!|
|[02](https://github.com/ConnorY97/DreadEngineMk3/commit/af651eda5954f7ef4d4766aa2917fa4a241d7d06)|Updating VS broke everything!. Everything broke, nothing was linked or included I hate external stuff!|
|[03](https://github.com/ConnorY97/DreadEngineMk3/commit/7fb55d08e6aa5764d63eba2c0e6dbfdf41ed27aa)|Update|
|[04](https://github.com/ConnorY97/DreadEngineMk3/commit/186d19cc612b14f01dd3c27f6ecb7b74bc748224)|Update|
|[05](https://github.com/ConnorY97/DreadEngineMk3/commit/b9870daa3262563aa0a6a8c11e944364beadaba6)|Create Delta time|
|[06](https://github.com/ConnorY97/DreadEngineMk3/commit/d6369d134bbea128974ebe3f496da0139a1e0cef)|Creating quads|
|[07](https://github.com/ConnorY97/DreadEngineMk3/commit/da04cac0a89c4f2f4f589505fb3d959631a7bf31)|Added transforms|
|[08](https://github.com/ConnorY97/DreadEngineMk3/commit/3389c17c8c3225e870465db804051f68903afddd)|Quad holds the transform. Updates the shader  per quad with its transform information|
|[09](https://github.com/ConnorY97/DreadEngineMk3/commit/81cdf1a7f01504a8b4fbdc7d24077517700491a1)|Can move quads by updating position|
|[10](https://github.com/ConnorY97/DreadEngineMk3/commit/f1a9cc51d38722acb2fc272beb3f4a6ca19ea8ff)|Put quad creation into a vector. I can now make lots of quads much easier|
|[11](https://github.com/ConnorY97/DreadEngineMk3/commit/f827a58f1e5f665a62cd25288a2c319dffacbc81)|Added global QUADAMOUNT. This is to stop from either drawing or deleting more than exist|
|[12](https://github.com/ConnorY97/DreadEngineMk3/commit/d8ad7088f427e34d193d1af71fd4aca8dcead5d1)|Added Image loading and Texture Class|
|[13](https://github.com/ConnorY97/DreadEngineMk3/commit/b7aa1b69a16997a53897debf02dfbce59a77fe39)|Textured Quads|
|[14](https://github.com/ConnorY97/DreadEngineMk3/commit/dd5445641fc3227a61fe9b1e15e18c3abdd984e7)|Attempting to add more textures|
|[15](https://github.com/ConnorY97/DreadEngineMk3/commit/74b054d4c170230fcb6f9ef7f7b91be71a0f493a)|Fixing texture issues|
|[16](https://github.com/ConnorY97/DreadEngineMk3/commit/aed39da822829add593f923cf8a94a7403293c82)|Done quite a bit. Now you can add ballz on the fly,. Thinking of adding a square class so that it can have hp to correspond with its color.. Currently working state|
|[17](https://github.com/ConnorY97/DreadEngineMk3/commit/3130b51627a9e69b82aaad3c475f97f81daa1cd0)|Creation of Square Class|
