IMPORTANT: FOLLOW INSTALL INSTRUCTIONS!

## ADDITIONAL REQUIRED FILES:

Download this and extract as instructed in "installing" below
https://github.com/gavanw/vqisosmall/releases/download/0.1/resources.zip


## Voxel Quest Isometric

Voxel Quest is a project with several engine iterations. This is the very first engine iteration, and features isometric voxel rendering. See http://www.voxelquest.com for more info.

Note that this is the earliest engine iteration and many fixes have been made since then, but there is also high demand for the isometric version of the engine so I am releasing that first in spite of the fact that it is the least polished iteration.

This is a very, very, VERY rough release. There are many things wrong with the way this project is organized currently, and I am well aware of most of them but feel free to comment. A few things that are wrong: use of absolute paths (edit: now fixed by another user, please credit yourself I lost the commit info during the wipe), including all dependencies within the same project folder, unnecessary files in the repository, an all-around messy project structure, etc. In short, this thing is more fun than a jar full of angry bees!

The code is also not that well organized, but I will try to explain it as best I can.

Anyhow, I just want to get something out - I can't spend all of my time perfecting releases, and I think everyone would be better served to get the releases sooner. I will leave cleanup as an exercise to contributors and help to the best of my ability :) 

## Installation

Recommended: Windows 7+, 16+ gigabytes of RAM, GTX 780+, but it should run on less.

If you wish to separate out the requirements, it uses SFML 2.1. If you wish to utilize Poco (for networking), it uses an older version of poco and you must define USE_POCO in the code.

Steps:

1) install git as needed (duh!)

2) create the parent folder where you want to store this repository (note that there will likely be more versions in the future, so you may want one folder to store all of them)

3) open cmd and navigate this folder

4) type "git clone https://github.com/gavanw/vqisosmall.git"

5) type "cd vqisosmall"

6) type "explorer ."

7) extract "resources.zip" to this folder (this link to this file is at the top of this readme)

8) open "GLSLFragmentLighting.sln"

9) Make sure build is set to "Release" and "x64" (may likely default to debug/win32 which is bad)

## Building 

VQ uses automatic header generation (via lzz) and also concatenates files and performs other operations with batch scripts. The output file is located in compiled/main.cpp (useful for debugging). However, you should not edit this file as it is generated, you must edit the files that it is based off of (i.e. if you double click on an error in Visual Studio, it will bring up the generated file). The proper workflow is to edit the files within the src folder then run the build (which will generate the large, linear main.cpp file). If you do not like working with generated code, you can always generate it once then disable the scripts and edit the output file(s) by hand.

The rationale for lzz and file concatenation can be found in the links below.

http://stackoverflow.com/a/318440

http://stackoverflow.com/a/373179

In addition, header generation reduces the amount of code you need to maintain (and the number of file locations you must navigate between). Generation with concatenation simplifies the entire use of headers and relieves users of the responsibility of managing include directives. Files are concatenated in alphabetical / numerical order. In other builds I have better forward declaration of headers, inline.




Open "GLSLFragmentLighting.sln" in Visual Studio Express 2012 (https://www.microsoft.com/en-us/download/details.aspx?id=34673)

Simply run "Build Solution" - this will automatically invoke the required scripts during the appropriate build steps.

Prepare for errors! I have only tested this build on two machines!

## Notes on the code

Most things you will want to adjust (constants and such) are either located in the Singleton class (f00300_singleton.hpp) or includes.h (f00025_includes.h). And yes, I am aware that the use of global constants is not necessarily best practice but it was never intended to be permanent. :) Note that the numbers before the files ensure the order in which they get concatenated. Concatenation makes include directives a no-brainer and also speeds up compilation. If you need to use the include directive, it should only need to be done within includes.h. Otherwise, the automatic header generation should handle your needs (all files ending in .hpp automatically have headers generated for them, otherwise the file is concatenated as-is).

My vector class is really crappy (FIVector4) - it was intended to be a hybrid int/float 1-4 dimensional vector (basically, an uber vector) so that I could use one class for all vector types.  It lacks operator overloading and is purely functional (ugh). Later engine iterations make heavier use of Bullet Physics' vector class, and Song Ho's vector/matrix classes (http://www.songho.ca/opengl/gl_matrix.html)

## Running

Executable is located in the bin folder, if not compiling.

Default controls:

Mouse + Left Button (LB): pan along the XY (ground) plane

Mouse + Right Button (RB): pan along the Z axis (HIGHLY recommended you figure out how to do this - it will load chunks around your the center of your camera location, and for all you know your camera may be way above or below where you want to load chunks - hard to tell in isometric mode but the fog does provide minor depth cues)

Mouse Wheel: zoom out (zoom out really far to get to the map, where you can pan to a new location using same controls above - HIGHLY recommended you do this on bootup, as it will likely spawn you somewhere random like the middle of an ocean)

Ctrl: show control boxes. This will bring up boxes you can manipulate using the above, while holding down ctrl. The green box controls the cutaway, the white box controls the light, the blue box controls the fog.

g: toggle edit modes: 0: no editing, 1: edit voxels (click several times with LB to add voxels, RB to remove voxels), 2: edit buildings

s: toggle macro edit mode (for edit mode 1), makes bigger chunks of terrain

d: toggle day/night

p: toggle fullscreen

tab: toggle menu

c: clear/refresh scene

r: refresh shaders

f: fog on/off

A (capital A): increase chunk load radius

Z (capital Z): decrease chunk load radius

v (while in edit mode 2): toggle building visibility

l: turn on multiple colored lights for testing (hold down ctrl to see them and move them)

e: set camera to nearest elevation

[ and ]: decrease/increase detail (shadow steps, AO steps, radiosity steps)

esc (press several times): exit

## Contributing

TBD, but for now feel free to fork it and do whatever. :)

## Authors
Gavan Woolery (http://www.twitter.com/gavanw)
[ADD YOURSELF DIRECTLY ABOVE HERE, with an optional link]

## Additional Credits

Special Thanks: the 1500+ Kickstarter backers and patrons who made this possible, and my investors for allowing me to open source this.

## FAQ

q) I cannot find a way to change thing XYZ while playing the game
a) It is probably hard-coded (cringe) - jump into the code!

## License

The license for Voxel Quest is MIT (if for some reason this does not work for you, I can grant permission to use another).

The license for FreeGlut, Glew, SFML, and Poco (not actively used but deprecated references exist) all fall under the licenses of the repsective holders.

Inventory/NPC/Monster icons were purchased/licensed from 7Soul on gamedevmarket.net:
(If you use any of these icons you must purchase your own copy)

http://www.gamedevmarket.net/asset/16x16-icons-for-rpg-pack-1-915/

Logo fonts are based on work from Daniel Guldkran's Free Fonts Online site:

http://www.algonet.se/~guld1/freefont.htm

Nature sounds are under the CC BY 3.0 License from:

http://archive.org/details/Sounds_of_Nature_Collection

All other sounds and instruments were from:

http://tracker.modarchive.org/

Almost all of the code and other resources were created by me, a few things were scraped from public resources (Stack Overflow, tutorials, etc). If you see something that should be under a license but is not, please let me know.
