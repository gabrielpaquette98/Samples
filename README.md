Hello there!

This is a simple repository to show some of the things I made for fun.

## Space Distortion
![Space Distortion](https://github.com/gabrielpaquette98/Samples/blob/main/gifs/SpaceDistortion.gif)

Distorting space in a manner that isn't doable outside of computer graphics is something that always fascinated me. This is an example of vertex displacement and deformation to create an effect akin to gravity, or reality, bending to clear a sphere around a position. Notice how some objects are moved completely and how some on the green perimeter are only deformed within the perimeter. 

Taken further, the same code can be applied to deform a terrain, and with an added particle system to represent a ring around the perimeter, it now looks like this:
![Space Distortion 2](https://github.com/gabrielpaquette98/Samples/blob/main/gifs/SpaceDistortion2.gif)

## Procedural Animation
![Procedural Animation](https://github.com/gabrielpaquette98/Samples/blob/main/gifs/ProceduralAnimation.gif)

This is an example of procedural animation with a four-legged example object. A lot of other examples online made me want to try it out. It uses inverse kinematics, and the legs are moved according to predetermined groups of legs. It adapts to irregularities in heights and slopes. 

## Dog Character
![Dog Character](https://github.com/gabrielpaquette98/Samples/blob/main/gifs/Dog.gif)

This is a dog I modeled to test ideas with four-legged locomotion and animation. I rigged it and animated it (including walking/running cycles not shown here). I used it to test a few things, including a spring-based hovering character controller. Instead of relying on a direct contact with the ground, a raycast determines the distance from the ground and follows physics principles of springs to maintain a hovering distance from the ground. I tested a few ideas from there: using springs on each leg to have a more natural movement of the dog when it walks, procedural animation to move the legs, blending procedural animation and my previously made animations, inverse kinematics so that the paws always match the terrain, and using avatar masks to separate the animations on different body parts.

## Humanoid Character
![Humanoid Character](https://github.com/gabrielpaquette98/Samples/blob/main/gifs/CharacterA.gif)

I felt like making a character, and once it was in a working state, I used it to try out some of Mixamo's features. I modeled this character, taking some inspiration from Miis and low-poly art, and tried out Mixamo's auto-rigging and animations.  

