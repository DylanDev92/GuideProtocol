# EntityCollections

Using an EntityCollection, you can easily iterate over all the entities in the group and perform operations on them as a whole. This can be useful for things like updating and checking player data/properties. For example, if you have a game with NPCs and players, you can use filters to perform operations on just the NPCs or just the players. This can be useful if you want to update the behavior of all NPCs of a certain type, or if you want to check the health of all players in a certain area.

- `EntityCollections.RandomPlayer;` For getting a random player.
- `EntityCollections.RandomNPC;` For getting a random NPC.
- `EntityCollections.RandomEntity;` For getting a random entity.
- `EntityCollections.Accounts;` For getting a list of accounts.
- `EntityCollections.Entities;` For getting a list of entities.
- `EntityCollections.Humans;` For getting a list of human-players.
- `EntityCollections.NPCs;` For getting a list of npcs.
- `EntityCollections.FindByID(int);` Returns an entity by its ID.
- `EntityCollections.TryFindByID(int, out ShEntity);` Returns a bool to check, and has an ShEntity out parameter.
- `EntityCollections.TryGetPlayerByNameOrID(string, out ShPlayer);` Returns a bool to check, and has a ShPlayer out parameter.

# Show a player list

In this example we're going to use `EntityCollection.Humans` in a foreach to add the player usernames to a list `List<string>` and then display them in a text panel `player.svPlayer.SendTextMenu()` in game. This will be executed with a command `CommandHandler.RegisterCommand();`.

[](src/EntityCollections.mp4 ':include :type=video controls width=100%')

```cs
public class PlayerListCollection : IScript
{
    public PlayerListCollection()
    {
        CommandHandler.RegisterCommand("PlayerCollections", new Action<ShPlayer>(ShowPlayerList));
    }
    public void ShowPlayerList(ShPlayer player)
    {
        List<string> playersInGame = new List<string>();
        foreach (ShPlayer p in EntityCollections.Humans)
        {
            playersInGame.Add(p.username);
        }
        player.svPlayer.SendTextMenu("Players online", string.Join("\n", playersInGame));
    }
}
```

# Show a list of players with a determined job

In this example we're going to do the same as above but the difference is that we're going to use [`System.Linq`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.where) to "filter" them using `Where()` which basically returns a list of the elements that match with certain conditions.

[](src/EntityCollectionsPolices.mp4 ':include :type=video controls width=100%')

```cs
public class PlayerListCollection : IScript
{
    public PlayerListCollection()
    {
        CommandHandler.RegisterCommand("ShowPolices", new Action<ShPlayer>(ShowPolices));
    }
    public void ShowPolices(ShPlayer player)
    {
        List<string> policesInGame = new List<string>();
        foreach (ShPlayer p in EntityCollections.Humans.Where(x => x.svPlayer.job.info.shared.jobName == "Police"))
        {
            policesInGame.Add(p.username);
        }
        player.svPlayer.SendTextMenu("Polices online", string.Join("\n", policesInGame));
    }
}
```