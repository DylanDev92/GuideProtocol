# CommandHandler
> `CommandHandler` is a class that we will use its different methods to create/modify commands.

Before starting we're going to make a new class, you can choose the name you want. Inside of the class we're going to add the `IScript` and create a constructor to execute RegisterCommand() which will create a command. `CommandHandler.RegisterCommand("CommandName", Action<ShPlayer>())` inside of those parenthesis we're going to give a method that has the same parameters as the arguments we gave in `Action`.

This video shows how to make a command that says "Hello World!" in the player's chat.

[](src/PluginCommandHandler.mp4 ':include :type=video controls width=100%')

`shPlayer.svPlayer.SendGameMessage("Hello World!");` `SendGameMessage` is used for sending a message to the player.
```cs
class TestCommand : IScript
{
    public TestCommand()
    {
        CommandHandler.RegisterCommand("SayHello", new Action<ShPlayer>(SayHelloToPlayer));
    }
    public void SayHelloToPlayer(ShPlayer shPlayer)
    {
        shPlayer.svPlayer.SendGameMessage("Hello World!");
    }
}
```

# Lets use parameters
We're going to do the same as before but this time adding some data types, the most common to use is `string`, but you can also use `int` `float` `byte` whatever you need for the command. All you have to make sure is that the method and the register command parameters match.

[](src/PluginCommandHandler1.mp4 ':include :type=video controls width=100%')

`InterfaceHandler.SendGameMessageToAll(message);` `SendGameMessageToAll` is used for sending a message to all the players.
```cs
class TestCommand : IScript
{
    public TestCommand()
    {
        CommandHandler.RegisterCommand("MessageToEveryone", new Action<ShPlayer, string>(MessageToEveryone));
    }

    public void MessageToEveryone(ShPlayer shPlayer, string message)
    {
        InterfaceHandler.SendGameMessageToAll(message);
    }
}
```

# Example of player message
In this example we're going to make a command where we get a player from a string and then we're going to send it a message. We're going to use `EntityCollections` to get a player from an ID/Username with the method `TryGetPlayerByNameOrID` that method returns a `bool` so we can check if the player is valid or not and determine if the command is going to continue or not. Also that method has an `out` parameter, we're going to use that as the gotten player.

[](src/PluginCommandHandler2.mp4 ':include :type=video controls width=100%')

There will be a section specifically about `EntityCollections`
```cs
class TestCommand : IScript
{
    public TestCommand()
    {
        CommandHandler.RegisterCommand("SendMessageToPlayer", new Action<ShPlayer, string, string>(MessageToPlayer));
    }

    public void MessageToPlayer(ShPlayer shPlayer, string player, string message)
    {
        if (EntityCollections.TryGetPlayerByNameOrID(player, out ShPlayer playerOut))
        {
            playerOut.svPlayer.SendGameMessage(shPlayer.username + "Sent you: " + message);
        }
        else
        {
            shPlayer.svPlayer.SendGameMessage("Player not found");
        }
    }
}
```