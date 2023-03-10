# Entities
You can search for default entities in [3D entities](https://r00t.brokeprotocol.com/assetbrowser/).

An entity can be an item, a player, an NPC. Basically any object that contains the scripts Entity.

For getting an entity you can use:

- `SceneManager.Instance.TryGetEntity(int/string, out ShEntity entity)` This is useful if the object may be null.
- `SceneManager.Instance.TryGetEntity<ShVehicle>(int/string, out ShVehicle entity)` If you want a ShVehicle is also possible
- `SceneManager.Instance.GetEntity(int/string)` This returns a ShEntity.
- `SceneManager.Instance.GetEntity<ShItem>(int/string)` If you want to return an ShItem is also possible.

# Spawn an entity
Lets spawn a car/vehicle, we're going to use `SvManager.Instance.AddNewEntity()`to add the vehicle to the map and we're going to give it the player's position, place, and rotation so it spawns on the player. This process would also work with whatever entity you want to spawn.

```cs
public class GettingEntities : IScript
{
    public GettingEntities()
    {
        CommandHandler.RegisterCommand("SpawnCar", new Action<ShPlayer, string>(SpawnCar));
    }
    public void SpawnCar(ShPlayer player, string carName)
    {
        if (SceneManager.Instance.TryGetEntity(carName, out ShVehicle entity))
        {
            SvManager.Instance.AddNewEntity(entity, player.GetPlace, player.GetPosition, player.GetRotation, false);
        }
    }
}
```

# Give an item
Lets get an item and then give it to the player. First thing we have to do is get the entity this must be ShItem or related, then we're going to use `TransferItem()` to tranfer the player that item.

```cs
public class GettingEntities : IScript
{
    public GettingEntities()
    {
        CommandHandler.RegisterCommand("GiveItem", new Action<ShPlayer, string>(GiveItem));
    }
    public void GiveItem(ShPlayer player, string carName)
    {
        if (SceneManager.Instance.TryGetEntity(carName, out ShItem item))
        {
            player.TransferItem(DeltaInv.AddToMe, item, 1);
        }
    }
}
```