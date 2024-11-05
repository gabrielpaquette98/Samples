Hello there!

I made this page to show some of the things I made for fun:

## Procedural Generation

This is a subject that fascinated me since the first time I played Minecraft. During my studies as a software engineer, one of the first things I tried was making a clone of this game in the Unity engine. I quickly started to add my own ideas and focused on a round world.

### Isocahedron
![Isocahedron](https://github.com/gabrielpaquette98/Samples/blob/main/assets/IsocahedronV1.gif)

This is my first iteration of a round, procedurally generated planet. It's based on a simple isocahedron, and each face is subdivided into multiple chunks according to a few parameters. Each chunk is then subdivided into multiple triangles, and when each triangle is made, its vertices are deformed according to a series of differently parameterized noise passes. This deformation contains a pass that generates big mountains and valleys, and two other passes to generate finer details, which can be seen on the mountain tops. Each chunk is then assigned a color based on how high it is relative to the center of the planet, and a simple blue sphere represents the water. The subdivided isocahedron is an interesting technique, but it makes adding caves and tunnels a harder task since it just deforms a surface. The next approach I tried out mostly removes this difficulty.

### Marching Cubes and Density Array
![Marching Cubes](https://github.com/gabrielpaquette98/Samples/blob/main/assets/ShadedMarchingCubes.gif)

This second iteration uses a three-dimensional array of density values. These values represent whether a single unit of 3D space is filled or is empty. Each entry in the array is evaluated based on the position to determine if it is solid. This uses the same noise passes as the previous iteration. Depending on the result of these noise passes, a specific position in the 3D array may be solid or not, which is then used by the Marching Cubes algorithm to generate a mesh. Depending on the neighboring entries in the density array, a configuration is picked to fill the current cube. Each cube is evaluated, and the triangles are added to a chunk's mesh. The result is a completed mesh representing the density array, in this case the density described the spherical planet by using noise passes. The shading is done differently from before, a specific height from the center of the planet is used to sample a gradient.


### Generating 2D dungeons

![Escape The Angamando](https://github.com/gabrielpaquette98/Samples/blob/main/assets/EscapeTheAngamando.png)

During a game jam, I made an algorithm to generate a 2D maze-like dungeon with rooms randomly pieced together and then placed in a similar structure as the first Zelda game or as The Binding of Isaac. The game, filled with bugs and anything that comes with making a game in two days with little sleep, can be played here: https://gabendalf.itch.io/escape-the-angamando . The project evolved and eventually became an important project at Poly Games, a student association about making games at Polytechnique Montreal. I launched the project with another student, and I remade the entire level generation algorithm, it would now be based on 4x4 floor pieces, allowing for narrow hallways as well as bigger rooms, with the walls being added after generating the layout. It started out as a text-based prototype, and eventually was integrated into Unity. The screenshot shows a version of the first level. It can be randomly regenerated from the editor with a button, the 4x4 floor piece can be set to any size, and the algorithm that places these pieces can be entirely replaced, as well as which assets it uses. The Strategy design pattern was implemented to allow any other student to implement their own strategy for placing the floor pieces and adapt it to different contexts, like levels in a forest or in a cave. The current strategy shown in the screenshot is the "Branching Out" strategy: it starts at a specific location, it randomly invalidates neighboring floor positions and places a floor piece where it can. Based on the parameters, it can generate more hallways or bigger rooms. Walls are then placed, a starting and a finishing floor piece is selected, and the level starts.


## Cel Shading

When learning at school how OpenGL and shaders work, a teacher mentioned how cel shading works as an example of fragment shader. The topic interested me, so I implemented it as described in OpenGL. Later, I used Shader Graph in Unity to port this specific shader. The first result, when applied to a modified version of a humanoid character I made, gave me this:

![Basic Cel Shading](https://github.com/gabrielpaquette98/Samples/blob/main/assets/CelShading-StraightToShaderGraph.png)

It was a very basic version of cel shading. It couldn't handle lights or shadows at all, but the principles were there: a light source is used with a dot product to determine how much intensity a specific fragment should have, and a sharp color ramp is multiplied to the color to achieve a cel shaded look. I decided to improve on it and made the following versions:

![Cel Shading](https://github.com/gabrielpaquette98/Samples/blob/main/assets/CelShading.png)

![Cel Shading Outline](https://github.com/gabrielpaquette98/Samples/blob/main/assets/CelShadingLined.png)

![Lit Cel Shading](https://github.com/gabrielpaquette98/Samples/blob/main/assets/CelShadingLit.png)

![Lit Cel Shading Outline](https://github.com/gabrielpaquette98/Samples/blob/main/assets/CelShadingLitLined.png)

The first two versions add a bright highlight by adding a second gradient on top of multiplying the color to the ramp gradient, which gives a much less flat look.

The last two versions react better to shadows, and the highlight is implemented differently. Instead of an added gradient, it works by using a Fresnel effect multiplied by the dot product of the normal of the fragment and the light direction. Instead of adding a brighter cel, it adds a more realistic increase in light intensity based on where the light is.  

The Fresnel effect is a very versatile effect, and by using it to sample a gradient, it is very easy to make the outline seen on the sphere. However, this method of making an outline does not necessarily produce a perfect outline on more complex models like this character. It adds many thicker or thinner lines depending on the normals, and it could make a very stylized outline if it is used alongside another outline method that produces a minimum outline thickness. It reminded me about the bold outlines from [Okami](https://www.gamehype.co.uk/wp-content/uploads/2017/09/okami-hd-1280x640.jpg), a very beautiful and stylized game.

## Space Distortion
![Space Distortion](https://github.com/gabrielpaquette98/Samples/blob/main/assets/SpaceDistortion.gif)

Distorting space in a manner that isn't doable outside of computer graphics is something that always fascinated me. This is an example of vertex displacement and deformation to create an effect akin to gravity, or reality bending to clear a sphere around a position. Notice how some objects are moved completely and how some on the green perimeter are only deformed within the perimeter. 

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

