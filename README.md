Hello there!

I made this page to show some of the things I made for fun:

## Sea of triangles
![Sea of triangles](https://github.com/gabrielpaquette98/Samples/blob/main/assets/DigitalSea.gif)

This one was to try out geometry shaders for the first time. It also renders all the triangles with a unique color into a buffer that is then used to generate the white outlines, any pixel in that buffer with neighbors of different colors generates a white outline in a post processing pass. 

## Équistellaire
https://github.com/user-attachments/assets/004eb1e5-85a9-432c-8b94-9769d0716ad2

Équistellaire is a game I made in two days during a game jam with two other programmers and a sound designer. I felt like it needed an effect that would indicate that the level is wiped and changed to a new level with a new layout, so I made the effect where the stars rotate and stretch between each level. It was a bit before I got into shaders and post processing passes so it uses a TrailRenderer for each star. It's not quite optimized, but it got the job done for the jam!


## Procedural Generation

### Isocahedron
![Isocahedron](https://github.com/gabrielpaquette98/Samples/blob/main/assets/IsocahedronV1.gif)

This is my first iteration of a round, procedurally generated planet. It's based on a simple isocahedron, and each face is subdivided into multiple chunks according to a few parameters. Each chunk is then subdivided into multiple triangles, and when each triangle is made, its vertices are deformed according to a series of differently parameterized noise passes. This deformation contains a pass that generates big mountains and valleys, and two other passes to generate finer details, which can be seen on the mountain tops. Each chunk is then assigned a color based on how high it is relative to the center of the planet, and a simple blue sphere represents the water. The subdivided isocahedron is an interesting technique, but it makes adding caves and tunnels a harder task since it just deforms a surface. The next approach I tried out mostly removes this difficulty.

### Marching Cubes and Density Array
![Marching Cubes](https://github.com/gabrielpaquette98/Samples/blob/main/assets/ShadedMarchingCubes.gif)

This second iteration uses a three-dimensional array of density values. These values represent whether a single unit of 3D space is filled or is empty. Each entry in the array is evaluated based on the position to determine if it is solid. This uses the same noise passes as the previous iteration. Depending on the result of these noise passes, a specific position in the 3D array may be solid or not, which is then used by the Marching Cubes algorithm to generate a mesh. Depending on the neighboring entries in the density array, a configuration is picked to fill the current cube. Each cube is evaluated, and the triangles are added to a chunk's mesh. The result is a completed mesh representing the density array, in this case the density described the spherical planet by using noise passes. The shading is done differently from before, a specific height from the center of the planet is used to sample a gradient.


## Characters
![Human Character](https://github.com/gabrielpaquette98/Samples/blob/main/assets/CharacterA.gif)

This was the first human character I ever made. I felt like making a character so I made one in Blender, and I used it to try out some of Mixamo's features. I modeled this character, taking some inspiration from Miis and low-poly art, and tried out Mixamo's auto-rigging and animations to get a first experience for integrating a full character into Unity.   

![Dog Character](https://github.com/gabrielpaquette98/Samples/blob/main/assets/Dog.gif)

I made this dog to test ideas for four-legged locomotion and animation. I rigged it and animated it (including walking/running cycles not shown here). I used it to test a few things, including a spring-based hovering character controller. Instead of relying on a direct contact with the ground, a raycast determines the distance from the ground and follows physics principles of springs to maintain a hovering distance from the ground. I tested a few ideas from there: using springs on each leg to have a more natural movement of the dog when it walks, procedural animation to move the legs, blending procedural animation and my previously made animations, inverse kinematics so that the paws always match the terrain, and using avatar masks to separate the animations on different body parts.

![Roller](https://github.com/gabrielpaquette98/Samples/blob/main/assets/Roller.gif)

My second human character, this time I wanted to do the rigging and animating myself, and give it more detail now that I was a bit used to Blender. I wanted to get a better idea of what a full character pipeline needs, including modeling, rigging, animating and integrating. I did a few animations like this one, it's quite a bit stiff but I got to learn a lot from it. 

![Knight](https://github.com/gabrielpaquette98/Samples/blob/main/assets/Knight.gif)

My third human character, except this time I tried to do it much faster, and improve on topology, and rely on bone constraints like inverse kinematics for placing the hands and feet as well as aiming the head.  


## Generating 2D dungeons

![Escape The Angamando](https://github.com/gabrielpaquette98/Samples/blob/main/assets/EscapeTheAngamando.png)

During a game jam, I made an algorithm to generate a 2D maze-like dungeon with rooms randomly pieced together and then placed in a similar structure as the first Zelda game or as The Binding of Isaac. The game, filled with bugs and anything that comes with making a game in two days with little sleep, can be played here: https://gabendalf.itch.io/escape-the-angamando . The project evolved and eventually became an important project at Poly Games, a student association about making games at Polytechnique Montreal. I launched the project with another student, and I remade the entire level generation algorithm, it would now be based on 4x4 floor pieces, allowing for narrow hallways as well as bigger rooms, with the walls being added after generating the layout. It started out as a text-based prototype, and eventually was integrated into Unity. The screenshot shows a version of the first level. It can be randomly regenerated from the editor with a button, the 4x4 floor piece can be set to any size, and the algorithm that places these pieces can be entirely replaced, as well as which assets it uses. The Strategy design pattern was implemented to allow any other student to implement their own strategy for placing the floor pieces and adapt it to different contexts, like levels in a forest or in a cave. The current strategy shown in the screenshot is the "Branching Out" strategy: it starts at a specific location, it randomly invalidates neighboring floor positions and places a floor piece where it can. Based on the parameters, it can generate more hallways or bigger rooms. Walls are then placed, a starting and a finishing floor piece is selected, and the level starts.


## Space Distortion
![Space Distortion](https://github.com/gabrielpaquette98/Samples/blob/main/assets/SpaceDistortion.gif)

Distorting space in a manner that isn't doable outside of computer graphics is something that always fascinated me. This is an example of vertex displacement and deformation to create an effect akin to gravity, or reality bending to clear a sphere around a position. Notice how some objects are moved completely and how some on the green perimeter are only deformed within the perimeter. 

Taken further, the same code can be applied to deform a terrain, and with an added particle system to represent a ring around the perimeter, it now looks like this:
![Space Distortion 2](https://github.com/gabrielpaquette98/Samples/blob/main/assets/SpaceDistortion2.gif)


## Procedural Animation
![Procedural Animation](https://github.com/gabrielpaquette98/Samples/blob/main/assets/ProceduralAnimation.gif)

This is an example of procedural animation with a four-legged example object. A lot of other examples online made me want to try it out. It uses inverse kinematics, and the legs are moved according to predetermined groups of legs. It adapts to irregularities in heights and slopes. 

