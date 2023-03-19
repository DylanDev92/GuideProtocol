# Simple jobs
We can make simple jobs in the file "LifeSource Jobs.json" we can copy an element from it and just paste it at the end.

The colors are RGB, if you have the 255 format you can just divide your numbers by 255 and get the decimal.

Is very important to put it at the end so we don't mess up with another jobs. We can count from 0 to the job we job created to get the jobIndex and give it to an boss NPC to get the job.

If you want a template of a basic job:
```json
{
    "groupIndex": "Citizen",
    "spawnRate": 0.0,
    "poolSize": 0,
    "transports": [
      {
        "transports": []
      },
      {
        "transports": []
      },
      {
        "transports": []
      }
    ],
    "randomEntities": null,
    "shared": {
      "jobName": "ExampleJob",
      "jobDescription": "Description of the example job",
      "jobColor": {
        "r": 1.0,
        "g": 0.5,
        "b": 0.0
      },
      "upgrades": [
        {
          "maxExperience": 0,
          "items": [
            {
              "itemName": "TeeLove",
              "count": 1
            },
            {
              "itemName": "PantsGray",
              "count": 1
            }
          ]
        }
      ]
    },
    "jobClassName": "Citizen",
    "characterType": "All",
    "maxCount": 0
}
```

## Coded jobs
Soon... [Official Guide](https://broke-protocol.github.io/broke-protocol/#/Jobs)