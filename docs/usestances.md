# Use Stances
A stance is the current state of the player, you can change it, read it, etc...

You can get the current stance with `ShPlayer.stance`

This are the stances of the player:
- `Stand`
- `Crouch` 	
- `SitMovable` 	
- `SitFixed` 	
- `SitMotorcycle` 	
- `SitKart` 	
- `Parachute` 	
- `Gunner` 	
- `Sleep` 	
- `KnockedDown` 	
- `Recovering` 	
- `KnockedOut` 	
- `Dead` 	
- `StandStill` 	
- `CrouchStill` 	
- `StandFixed` 	
- `CrouchFixed`

To set an instance we can use:

`ShPlayer.svPlayer.SvForceStance(StanceIndex)`

Some of the stances may not work on the players/npcs.

```cs
public void KO(ShPlayer player)
{
    player.svPlayer.SvForceStance(StanceIndex.KnockedOut);
}
public void Stand(ShPlayer player)
{
    player.svPlayer.SvForceStance(StanceIndex.Stand);
}
```