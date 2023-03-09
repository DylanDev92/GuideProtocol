# How to create a group
To create a group `groups.json` the first thing we have to do is to think which kind of group we need, there are:
- `AccountID` For account names/usernames.
- `ConnectionIP` For specific IPs.
- `JobName` For job names, useful for giving permissions to different jobs.
- `JobGroup` For job groups, also useful.

Let's make an example of a group named VIP and it is `AccountID` type, we're going to give it teleport and heal permissions, and give it a tag which is displayed in game.

`CustomData` Is useful sometimes, plugins like Essentials use it for formating the Global and LocalChat, you can use it however you want.

A `permission` is formed by the groupNamespace and the name of the permission. For example `bp.god`, every plugin has different permissions.
The `permission` `*` gives you all the permissions of all the plugins, if you want it specifically for a groupNamespace you can use for example `bp.*`
```
{
    "Type": "AccountID",
    "Name": "VIP",
    "Tag": "&4[VIP]",
    "Permissions": [
      "bp.teleport",
      "bp.heal"
    ],
    "CustomData": {
      "Data": {
      }
    },
    "Members": [
      "Dylan",
      "NongBenz"
    ],
    "Inherits": [
      "Default" <--- This is for inheriting the permissions of a group, in this case Default.
    ]
}
```

If you want to validate or check your JSON you can use this [JSON Validator](https://jsonlint.com/)
Remember to put properly the commas.

# Use CustomData in Code

We're going to use this group as example, we put an element "GroupMessage" that is an `string` that contains a message. What we're going to do is to make a command and get the primary group of the player, we can also get the group using [`System.Linq`](https://learn.microsoft.com/en-us/dotnet/api/system.linq).

```
{
    "Type": "AccountID",
    "Name": "Example",
    "Tag": "&4[Example]",
    "Permissions": [],
    "CustomData": {
      "Data": {
        "GroupMessage": "Hello example group!"
      }
    },
    "Members": [
      "Dylan"
    ],
    "Inherits": []
}
```

[](src/CustomDataGroup.mp4 ':include :type=video controls width=100%')

```cs
public class GroupCustomData : IScript
{
    public GroupCustomData()
    {
        CommandHandler.RegisterCommand("CustomData", new Action<ShPlayer>(GetCustomData));
    }
    public void GetCustomData(ShPlayer player)
    {
        string message = player.svPlayer.PrimaryGroup.CustomData.FetchCustomData<string>("GroupMessage");
        player.svPlayer.SendGameMessage(message);
        // We can also get the group with First()
        message = player.svPlayer.Groups.First(x => x.Name == "Example").CustomData.FetchCustomData<string>("GroupMessage");
        player.svPlayer.SendGameMessage(message);
    }
}
```

