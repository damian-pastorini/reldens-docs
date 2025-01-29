### Enemies experience rewards per level

This generator will create a file with the "experience rewards" by enemies per "variation" and "level".

The generator code can be found here: https://github.com/damian-pastorini/game-data-generator/blob/master/lib/generator/monsters-experience-per-level.js

There you can see how all the attributes below are used for the calculations.

Require parameters:
- "levelsExperienceByKey" or pass the levels experience file path when executing the command: this generator requires to know ALL the player levels experience data in the same format provided by the "levels generator".

This can be passed as plain JSON in the `levelsExperienceByKey` configuration, like:
```
{
    "1": {
        "req": 10,
        "total": 10,
        "growthFactor": 2
    },
    "2": {
        "diff": 10,
        "req": 20,
        "total": 30,
        "growthFactor": 2.005
    },
    //...
}
```
If you are passing the levels experience file path like `players-experience-per-level.json`, then you can keep avoid this parameter since it will be included by the generate command, see the following link:
https://github.com/damian-pastorini/reldens/blob/master/bin/generate.js#L141

- "variations": this has to include each variation key for which the experience has to be created with the corresponding value. 
```
{
    monsterA: 8,
    monsterB: 9,
    bossExtra: 15
}
```
As bigger the value is, the biggest the amount of given experience will be.
- "decrementProportionPerLevel": this property contains the values used to decrease the proportion of experience given per level, this way high level enemies will give less experience in proportion in order to increase the required kills count and by that making the leveling more difficult.
```
{
    '5': 0.8,
    '10': 0.42,
    '15': 0.4,
    '20': 0.26,
    '25': 0.15,
    '30': 0.1,
    '35': 0.08,
    '40': 0.0025
}
```

**IMPORTANT**: if you are using the `MonstersExperiencePerLevel` class in your own script, note the levels keys must be passed as "strings".

To use the generator follow these steps:

- Go to your game folder and create a folder called "generate-data".
- Inside the created folder create a new file named ["monsters-experience-per-level.json"](../examples/generate-data/monsters-experience-per-level.json).
- Save the following content in the file:
```json
{
    "levelsExperienceByKey": {
        "1": {
            "req": 10,
            "total": 10,
            "growthFactor": 2
        },
        "2": {
            "diff": 10,
            "req": 20,
            "total": 30,
            "growthFactor": 2.005
        },
        "3": {
            "diff": 20,
            "req": 40,
            "total": 70,
            "growthFactor": 2.01
        }
    },
    "variations": {
        "monsterA": 8,
        "monsterB": 9,
        "bossExtra": 15
    },
    "decrementProportionPerLevel": {
        "5": 0.8,
        "10": 0.42,
        "15": 0.4,
        "20": 0.26,
        "25": 0.15,
        "30": 0.1,
        "35": 0.08,
        "40": 0.0025
    }
}
```
This JSON contains the parameters that will be passed to the `monsters-experience-per-level` generator.

- Now open a console for the command line in your game folder.
- Run the following command:
```
$ npx reldens-generate monsters-experience-per-level ./generate-data/monsters-experience-per-level.json
```
And if you want to pass the experience by level using the file path, run this command:
```
$ npx reldens-generate monsters-experience-per-level ./generate-data/monsters-experience-per-level.json ./generate-data/players-experience-per-level.json
```
- As result, a new folder called "generated" will be created under your "game" folder, and there you will find a file with the generated data like:
```
{
    "1": {
        "req": 10,
        "total": 10,
        "growthFactor": 2,
        "monsterA": {
            "decrementProportion": 0,
            "randomVariation": 8,
            "exp": 1,
            "kills": 10
        },
        "monsterB": {
            "decrementProportion": 0,
            "randomVariation": 9,
            "exp": 1,
            "kills": 10
        },
        "bossExtra": {
            "decrementProportion": 0,
            "randomVariation": 15,
            "exp": 2,
            "kills": 5
        }
    },
    "2": {
        "diff": 10,
        "req": 20,
        "total": 30,
        "growthFactor": 2.005,
        "monsterA": {
            "decrementProportion": 0,
            "randomVariation": 8,
            "exp": 2,
            "kills": 10
        },
        "monsterB": {
            "decrementProportion": 0,
            "randomVariation": 9,
            "exp": 2,
            "kills": 10
        },
        "bossExtra": {
            "decrementProportion": 0,
            "randomVariation": 15,
            "exp": 3,
            "kills": 7
        }
    },
// ...
```
