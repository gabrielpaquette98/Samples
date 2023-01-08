Hello there!

This is a simple repository to show some of the things I made for fun.

## Procedural Generation

This is a subject that fascinated me since the first time I played Minecraft. During my studies as a software engineer, one of the first things I tried was making a clone of this game in the Unity engine. I quickly started to add my own ideas and focused on a round world.

### Isocahedron
![Isocahedron](https://github.com/gabrielpaquette98/Samples/blob/main/assets/IsocahedronV1.gif)

This is my first iteration of a round, procedurally generated planet. At first, it's a simple isocahedron, like a 20-sided dice, and each face is subdivided into multiple chunks according to a parameter. Each chunk is then subdivided into multiple triangles, and when each triangle made, its vertices are deformed according to a series of differently parameterized noise passes. This deformation contains a pass that generates big mountains and valleys, and two other passes to generate finer details, which can be seen on the mountain tops. Each chunk is then assigned a material based on how high it is relative to the center of the planet, and a simple blue sphere represents the water. The subdivided isocahedron is an interesting technique, but it makes adding caves and tunnels a harder task since it basically deforms a surface. The next approach I tried out mostly removes this difficulty.

### Marching Cubes and Density Array
![Marching Cubes](https://github.com/gabrielpaquette98/Samples/blob/main/assets/ShadedMarchingCubes.gif)

This second iteration uses a three-dimensional array of density values. These values represent whether a single unit of 3D space is filled or is empty. Each entry in the array is evaluated based on the position to determine if it is solid. The same noise passes as the previous iteration are used: the noise passes indicate the surface, if the entry is below the surface, then the density value is set to above the density threshold, so it becomes solid. A couple of other passes can be added, like adding rare resources into the ground. A previous version with a completely round surface had holes in it from a simple 3D noise function, resulting in a weird-looking planet. Once the density array is completed, it is then passed to a function that applies the Marching Cubes algorithm, a very interesting technique originally invented to visualize data from CT and MRI scans. My implementation reuses some lookup tables, but it mostly stays the same as the first version of the algorithm. Depending on the neighboring entries in the density array, a configuration is picked to fill the current cube. Each cube is evaluated, and the triangles are added to a chunk's mesh. The result is a completed mesh representing the density array, in this case the density described the spherical planet by using noise passes. The shading is done differently from before, this time it uses Shader Graph. A specific height from the center of the planet is determined as sand, and another is determined as snow. A simple gradient of colors is used, and each fragment uses a color within the gradient based on the distance from the fragment to the planet's core. 

## Space Distortion
![Space Distortion](https://github.com/gabrielpaquette98/Samples/blob/main/assets/SpaceDistortion.gif)

Distorting space in a manner that isn't doable outside of computer graphics is something that always fascinated me. This is an example of vertex displacement and deformation to create an effect akin to gravity, or reality, bending to clear a sphere around a position. Notice how some objects are moved completely and how some on the green perimeter are only deformed within the perimeter. 

Taken further, the same code can be applied to deform a terrain, and with an added particle system to represent a ring around the perimeter, it now looks like this:
![Space Distortion 2](https://github.com/gabrielpaquette98/Samples/blob/main/assets/SpaceDistortion2.gif)

## Procedural Animation
![Procedural Animation](https://github.com/gabrielpaquette98/Samples/blob/main/assets/ProceduralAnimation.gif)

This is an example of procedural animation with a four-legged example object. A lot of other examples online made me want to try it out. It uses inverse kinematics, and the legs are moved according to predetermined groups of legs. It adapts to irregularities in heights and slopes. 

## Dog Character
![Dog Character](https://github.com/gabrielpaquette98/Samples/blob/main/assets/Dog.gif)

This is a dog I modeled to test ideas with four-legged locomotion and animation. I rigged it and animated it (including walking/running cycles not shown here). I used it to test a few things, including a spring-based hovering character controller. Instead of relying on a direct contact with the ground, a raycast determines the distance from the ground and follows physics principles of springs to maintain a hovering distance from the ground. I tested a few ideas from there: using springs on each leg to have a more natural movement of the dog when it walks, procedural animation to move the legs, blending procedural animation and my previously made animations, inverse kinematics so that the paws always match the terrain, and using avatar masks to separate the animations on different body parts.

## Humanoid Character
![Humanoid Character](https://github.com/gabrielpaquette98/Samples/blob/main/assets/CharacterA.gif)

I felt like making a character, and once it was in a working state, I used it to try out some of Mixamo's features. I modeled this character, taking some inspiration from Miis and low-poly art, and tried out Mixamo's auto-rigging and animations.  

