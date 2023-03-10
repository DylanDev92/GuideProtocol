# What is JSON
JSON stands for "JavaScript Object Notation." is useful for a little database because it can store information in a structured format that can be easily read and manipulated. It is a versatile and flexible format that can handle a wide range of data types, including strings, numbers, arrays, and objects. This makes it an ideal choice for storing and retrieving data in a simple database.

This is a simple example of a JSON:
```json
{
  "name": "John Doe",
  "age": 35,
  "nationality": "American",
  "occupation": "Engineer",
  "address": {
    "street": "123 Main St",
    "city": "Anytown",
    "state": "CA",
    "zip": "12345"
  },
  "interests": ["reading", "hiking", "cooking"]
}
```

# Making a JSON
- For making a JSON the first thing you have to do is reference to `Newtonsoft.JSON`. Then the first thing we have to do is to make a new class with a name, in this case it's called `Configuration` and we're going to give some properties we can give later.
```cs
public class Configuration
{
    public string WelcomeMessage { get; set; }
    public int MoneyStart { get; set; }
    public bool EveryoneGod { get; set; }
}
```
- Next thing you have to do is to create a new `Configuration` object, then serialize it. `Serialization converts object data into a standardized format for storage or transmission. In this case a JSON`
```cs
public class UsingJson : IScript
{
    public UsingJson()
    {
        Configuration Config = new Configuration
        {
            WelcomeMessage = "Hello World!",
            MoneyStart = 1000,
            EveryoneGod = false
        };
        string serializedConfig = JsonConvert.SerializeObject(Config);
    }
}
```
- The serialization will return a string which is going to be stored/written as a JSON using `File.WriteAllText()` the path normally is `Path.Combine("Plugin", "NameOfJSON.json")` which will write the file in the Plugin's folder
```cs
public class UsingJson : IScript
{
    public UsingJson()
    {
        Configuration Config = new Configuration
        {
            WelcomeMessage = "Hello World!",
            MoneyStart = 1000,
            EveryoneGod = false
        };
        string serializedConfig = JsonConvert.SerializeObject(Config);
        File.WriteAllText(Path.Combine("Plugin", "Configuration.json"), serializedConfig);
    }
}
```
- Now that we have a JSON written we can read it using File.ReadAllText(), but this will return a string also, there's where deserialize comes `Deserialization is the process of converting a serialized object or data structure back into its original form or object, in this case a Configuration object`
```cs
public class UsingJson : IScript
{
    public UsingJson()
    {
        Configuration Config = new Configuration
        {
            WelcomeMessage = "Hello World!",
            MoneyStart = 1000,
            EveryoneGod = false
        };
        string serializedConfig = JsonConvert.SerializeObject(Config);
        File.WriteAllText(Path.Combine("Plugin", "Configuration.json"), serializedConfig);
        string readConfig = File.ReadAllText(Path.Combine("Plugin", "Configuration.json"));
        Configuration deserializedConfiguration = JsonConvert.DeserializeObject<Configuration>(readConfig);
    }
}
```
- We can set the deserialized object in a static object so it can be acessed in all the project.

```cs
public class UsingJson : IScript
{
    public static Configuration Config { get; set; }
    public UsingJson()
    {
        Configuration Config = new Configuration
        {
            WelcomeMessage = "Hello World!",
            MoneyStart = 1000,
            EveryoneGod = false
        };
        string serializedConfig = JsonConvert.SerializeObject(Config);
        File.WriteAllText(Path.Combine("Plugin", "Configuration.json"), serializedConfig);
        string readConfig = File.ReadAllText(Path.Combine("Plugin", "Configuration.json"));
        Config = JsonConvert.DeserializeObject<Configuration>(readConfig);
    }
}
```

# Compressed way to make a JSON
```cs
public class UsingJson : IScript
{
    public class Configuration
    {
        public string WelcomeMessage { get; set; }
        public int MoneyStart { get; set; }
        public bool EveryoneGod { get; set; }
    }
    public static Configuration Config { get; set; }
    public UsingJson()
    {
        File.WriteAllText(Path.Combine("Plugins", "Configuration.json"), JsonConvert.SerializeObject(new Configuration
        {
            WelcomeMessage = "Hello World!",
            MoneyStart = 1000,
            EveryoneGod = false
        }));
        Config = JsonConvert.DeserializeObject<Configuration>(File.ReadAllText(Path.Combine("Plugins", "Configuration.json")));
    }
}
```