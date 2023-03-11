# Toggling animations
Toggling animation of an object in Unity refers to the process of activating or deactivating an animation clip that has been applied to an object. This can be done changing the parameters/contition in a plugin. Toggling animation can be useful for a variety of reasons, such as creating interactive experiences where objects respond to user acations or changing the state of objects as you want.

We use these to change the parameters of the animation controller.
- `SvAnimatorBool()`
- `SvAnimatorFloat()`
- `SvAnimatorInt()`

Before starting if you don't know about animations in Unity I recommend you to take a tutorial in YouTube or wherever you want, and take a look to [Unity Animations](unityanimations.md).

First thing we have to do is create the animations, in my case I have 3 animations `ZeroState` you can call it however you want it's sometimes called `Idle` or `default` it's just the animation where the model/object is in it's original position, I also have an animation called `Move` which is going to move the object, and `Rotate` that rotates the object.

Next thing we have to do is to go to the `Animation Controller` and assign some parameters, this is pretty relative to what you want to do, You maybe want the 3 animations to have one specific parameter or several parameters to controll an animation. In this case we're making 2 parameters `isRotating` and `isMoving` which are going to be bool, we're going to make a transition from the `AnyState` to the animations we want, assign a parameter and change the properties as you want.

To clearify, the parameters can be `bool` `float` `int` you can use what you want, `float` for example is useful if you're triggering to a value that is constantly changing such as the speed of the player. `bool` is for more specific states I'd say.

Now we have to add `Entity` scripts to this object, then we're going to add a `Custom Action` on it, in this case it'll be `Rotate` and `Move`, next we have to assign the `Animator` in the `Animator field` of `ShEntity` and now we're good to go!

Remember to add a collider to the object we're moving.

[](src/ToggleAnimation.mp4 ':include :type=video controls width=100%')

Now we have the animations assigned to the object, now we have to export and let's go to `Visual Studio`

# Plugin/Script

As you know we used `Custom Actions` before, so now we're going to use the `ShEntity` that it gives us and activate the `BoolAnimation` using `SvAnimatorBool()`

[](src/ToggleAnimationScript.mp4 ':include :type=video controls width=100%')

```cs
public class ToggleAnimations : IScript
{
    [CustomTarget]
    public void RotateCreeper(ShEntity entity, ShPlayer caller)
    {
        entity.svEntity.SvAnimatorBool("isRotating", true);
        entity.svEntity.SvAnimatorBool("isMoving", false);
    }
    [CustomTarget]
    public void MoveCreeper(ShEntity entity, ShPlayer caller)
    {
        entity.svEntity.SvAnimatorBool("isMoving", true);
        entity.svEntity.SvAnimatorBool("isRotating", false);
    }
}
```

## Result

[](src/ToggleAnimationResult.mp4 ':include :type=video controls width=100%')