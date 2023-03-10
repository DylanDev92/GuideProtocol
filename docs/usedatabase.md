# How to read a Database
First of all, the database is located in:
- Windows: `C:\Users\YourName\AppData\LocalLow\CylinderStudios\BrokeProtocol`
- Linux: `.config/BrokeProtocol`

Use [LiteDB](https://www.litedb.org/) reading the databases that are in there.

[](src/Database.mp4 ':include :type=video controls width=100%')

# Interacting in Plugin
You can interact with the information of the database in code, get, update and maybe delete data. Remember to import `Lite.DB` in your references before starting.

## Getting version
```cs
var setting = svManager.Database.Settings.FindById("version");
Debug.Log(setting.Value) // Output: "1.0" 
```

## Getting player data
```cs
var user = svManager.Database.Users.FindById("Dylan");
Debug.Log(user.ID) // Output: "Dylan" 
Debug.Log(user.Character.BankBalance) //  Output: 7

svManager.Database.Users.Update(user); // For updating
```
- `ID`
- `IP`
- `PasswordHash` 
- `Profile`
- `LastUpdated` 
- `Persistent`
  - `AppContacts`
  - `AppBlocked`
  - `AppCalls`
  - `AppMessages`
  - `LastMessengers`
  - `UnreadMessages`
- `Character`
  - `BankBalance`
  - `AppTransactions`
  - `Job`
  - `Position`
  - `Rotation`
  - `MapName`
  - `SkinIndex`
  - `PlaceIndex`
  - `EquipableIndex`
  - `Attachments`
  - `Wearables`
  - `Items`
  - `Bindings`
  - `Apartments`
  - `Injuries`
  - `Stats`
  - `Health`
  - `KnockedOut`
  - `CustomData`

## Getting ban data
```cs
var ban = svManager.Database.Bans.FindOne(x => x.Username == "NongBenz");
Debug.Log(ban.Reason) // Output: "Massive RDM" 
```
- `IP`
- `Username`
- `Reason`
- `Time`

# Player CustomData
CustomData is a useful feature that lets you save information about a player in your plugin without using a separate JSON file. It allows you to store data on a per-player basis and retrieve it within your plugin's code, making your plugin more efficient.

- `player.svPlayer.CustomData["key"]` You can set and get data with this
- `player.svPlayer.CustomData.AddOrUpdate("key", value)` You can set/update data
- `player.svPlayer.CustomData.TryFetchCustomData("key", out int value)` You can get the data

```cs
public class UsingDatabase : IScript
{
    public UsingDatabase()
    {
        CommandHandler.RegisterCommand("MyAge", new Action<ShPlayer, int>(ChangeAge));
    }
    public void ChangeAge(ShPlayer player, int age)
    {
        // This works for getting and setting data
        player.svPlayer.CustomData["Age"] = 10;
        // This is for seting data
        player.svPlayer.CustomData.AddOrUpdate("Age", 10);
        // The way that I most recommend to fetch the custom data in case is null
        if (player.svPlayer.CustomData.TryFetchCustomData("Age", out int ageOut))
        {
            player.svPlayer.SendGameMessage("You are " + ageOut + " years old");
        }
        else // In case Age is null
        {
            player.svPlayer.SendGameMessage("You don't have age");
        }
    }
}
```