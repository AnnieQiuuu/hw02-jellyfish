# Procedural Jellyfish


## Project Overview
This project documents the creation of a fully procedural jellyfish in Houdini, combining node-based modeling, simulation, and rendering workflows.

### Result
[![Jellyfish video](./output.gif)](https://youtu.be/pwx2x5fgGWI)
### Features
- Jellyfish modeling
- Animation
- Lighting
- Rendering
<img height="500" alt="Jellyfish Parts" src="/assets/JellyfishParts.png">

## Veins
In order to create the veins for the jellyfish, you'll make use of the "Find Shortest Path" node. The Dungeon Corridor example in the Houdini Playground is a helpful reference for using this node. Here is some rough guidance for how to approach making the veins:

Remesh the jellyfish into triangles (otherwise you'll end up with very square looking veins)

<img width="300" alt="Remesh" src="/assets/Remesh.png">

Use the shortest path node to generate veins ([here](https://www.sidefx.com/docs/houdini/nodes/sop/findshortestpath.html) are the docs for the Find Shortest Path node)

<img width="300" alt="ShortestPath" src="/assets/ShortestPath.png">

Smooth out the veins for a more organic look. You might find yourself needing the "resample" and "fuse" nodes in addition to the "smooth" node (and remember, the [docs](https://www.sidefx.com/docs/houdini/nodes/sop/index.html) are a great resource if you're confused about what a node does or how to use it)

<img width="300" alt="ResampleFuseSmooth" src="/assets/ResampleFuseSmooth.png">

Use a "sweep" node to give the veins width

<img width="300" alt="Sweep" src="/assets/Sweep.png">

Lastly, stick the veins to the bell's animation using the "Point Deform" node that we used on the arms. The final result should look something like this:

<img width="300" alt="VeinsGif" src="/assets/VeinsGif.gif">

## Organs
The internal organs of the jellyfish were modeled procedurally with full creative freedom. Various geometry nodes and noise-based deformations were used to construct organic shapes, ensuring they integrated visually with the bell’s translucent structure.
<img width="300" alt="Organs" src="/assets/Organs.png">


## Tentacles
Creating the tentacles required abstracting generalizable techniques from a hair-simulation tutorial. Rather than replicating the workflow directly, the project focused on extracting relevant simulation principles and adapting them to Houdini.

<img width="300" alt="TentaclesGif" src="/assets/TentaclesGif.gif">

[This video](https://www.youtube.com/watch?v=LN4XXaHQkmU) demonstrates how to simulate hairs to create renders like this:

<img width="300" alt="HairRender3" src="/assets/HairRender1.png">
<img width="300" alt="HairRender2" src="/assets/HairRender2.png">
<img width="300" alt="HairRender1" src="/assets/HairRender3.png">


---

## Reference

[Geometry Nodes Documentation](https://www.sidefx.com/docs/houdini/nodes/sop/index.html)
[VEX Documentation](https://www.sidefx.com/docs/houdini/vex/functions/index.html)


## Houdini FAQ
[File Cache Node](https://www.youtube.com/watch?v=00s9YWDWFs0) - How do I use the File Cache node? Where does it save and how do versions work?
- Drop down the file cache node and the data will be save in disk. It saves time by caching the simulation data, so we don't need to recalculate everu time which saves time for rendering and playback.

[Simulation Caching](https://www.youtube.com/watch?v=jwIuzB9FkX0) - Why is my timeline turning blue/orange? Why isn't my simulation updating even though I made changes?
- Blue means houdini has all the geometry information cached in memory. Orange means the cache is out of the date. Houdini saves old information until users explicity tell it to update the information, cause sometimes we dont want to resimulate right after and freeze everything.

