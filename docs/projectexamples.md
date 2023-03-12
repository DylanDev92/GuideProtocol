# Some examples you can use to practice

# Assets
- Make a custom building with colliders.
- Make a gun or weapon.
- Make different consumables incluiding drugs.
- Make an animated statue an put it in the map.
- Make a processing table.
- Make a car.
- Make clothes.
- Make a new character.
- Make an entity with Interactive Events.

# Plugins
- Make a message system with different distance.
- When the player is spawned show a message.
- Make a kill leaderboard.
- Make moderation commands.
- Make a door system.
- Experiment with the damage event.
- Use triggerboxes to do something.
- Use OptionInputs or SubmitInputs to do something.
- Make a log system.
- Use coroutines to make delay commands.
- Make a bank system.

> The limit is your imagination! And Nong.

# TpAll

```cs
public void TpAll(ShPlayer player)
{
    foreach (ShPlayer p in EntityCollections.Humans.Where(x => x != player))
    {
        p.svPlayer.SvTeleport(player);
    }
}
```

# GiveAll

```cs
public void GiveAll(ShPlayer player, string itemName, int amount)
{
    foreach (ShPlayer p in EntityCollections.Humans)
    {
        p.TransferItem(DeltaInv.AddToMe, SceneManager.Instance.GetEntity(itemName).index, amount);
    }
}
```

# Self Knockout

```cs
public void Knockout(ShPlayer player)
{
    player.svPlayer.SvForceStance(StanceIndex.KnockedOut);
}
```

# Send message when joined

```cs
[Execution(ExecutionMode.Event)]
public override bool Ready(ShPlayer player)
{
    player.svPlayer.SendGameMessage("Hello, welcome to my server!");
    return true;
}
```

# Random number

```cs
public void RandomNumber(ShPlayer player)
{
    InterfaceHandler.SendGameMessageToAll(player.username + " sent a random number: " + Random.Range(0, 10).ToString());
}
```