### Players experience per level generator

This generator will create a file with all the "levels" required data so you can import them in Reldens.

The generator code can be found here: https://github.com/damian-pastorini/game-data-generator/blob/master/lib/generator/players-experience-per-level.js

Require parameters:
- "startExp": is the experience required to reach the first level.
- "baseGrowthFactor": this is the multiplier by which the previous level experience will be multiplied, and it's going to be incremented on each level iteration by the "growthIncrease" property.
- "baseGrowthFactorPerLevel": this is a container to specify a new "growthFactor" starting the specified level. 
Following the example below, this way if the initial growthFactor is 2, it will be applied until the level 5 when it changes to 1.5.
It is normal to decrease this value according the required experience increase, otherwise the required experience will get too high in the latest levels.
- "maxLevel": loop will generate data until this level inclusive.
- "growthIncrease": as noted above this value is used to increase the "baseGrowthFactor" per level iteration. 

To use the generator follow these steps:

- Go to your game folder and create a folder called "generate-data".
- Inside the created folder create a new file named "players-experience-per-level.json".
- Save the following content in the file:
```json
{
    "startExp": 10,
    "baseGrowthFactor": 2,
    "baseGrowthFactorPerLevel": {
        "5": 1.5,
        "10": 1.35,
        "15": 1.271,
        "20": 1.1,
        "40": 1
    },
    "maxLevel": 100,
    "growthIncrease": 0.005
}
```
This JSON contains the parameters that will be passed to the `players-experience-per-level` command.

- Open a console for the command line in your game folder. As next, we need to generate the ["levels"](update-link-here) for those sets.
- Run the following command:
```
$ npx reldens-generate players-experience-per-level ./generate-data/players-experience-per-level.json
```
- As result, a new folder called "generated" will be created under your "game" folder, and there you will find a file with the generated data like:
```json
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
    "3": {
        "diff": 20,
        "req": 40,
        "total": 70,
        "growthFactor": 2.01
    }
....
```
