# Simple Animations
In Unity, animations are created by defining an object's position, rotation, and scale over time. Animators control the playback of animations for game objects, while Animation Controllers are state machines that determine which animations should be played based on the game's current state. These tools allow game developers to create visually engaging and dynamic games with interesting movements and interactions.

In this example we're going to play this animation in game.

[](src/AnimationExample.mp4 ':include :type=video controls width=100%')

We're going to import the model inside the game, then we're going to right click on the model and create a "variant prefab", and we're going to edit it. Before selecting the animations we have to make sure that the model has the loop activated, otherwise only will be played once. Now we have to create a Animation Controller which is going to be used for playing the animations in game, next step we're going to add a "Animator" component inside of the object we have created, and drag the controller inside of it, inside of the animation controller we're going to add the animation that is inside of the model, make sure that is linked to the "Entry state". Now the animation should be played inside the game.

[](src/AnimationOpenClose.mp4 ':include :type=video controls width=100%')

# Using bones
In Blender, bones are a fundamental part of armature objects used for rigging and animating 3D models. Bones are particularly useful for animating because they allow you to create complex movements with a high degree of control. By linking the bones to the different parts of the mesh, you can manipulate the position, rotation, and scale of those parts in a more intuitive way than you could with just keyframe animation.

In this example we're going to animate this in Unity, remember to always export FBX. I'm not an expert in Blender so the model is going to be a little bit weird.

[](src/SimpleBones.mp4 ':include :type=video controls width=100%')

For using bones is almost the same, the difference is that instead of having different objects we're going to have individual bones.

[](src/AnimationBones.mp4 ':include :type=video controls width=100%')

This is how it looks in game, you can add colliders to the object so you can make the colliders move to make animated estructures, or whatever you want.

[](src/AnimationShow.mp4 ':include :type=video controls width=100%')