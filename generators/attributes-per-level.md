### Attributes per level generator

This generator will create a file that will list all the "levels", for each level it will generate a variation (these should be your class paths), and for each variation it will give you every "stat" value increment.

The generator code can be found here: https://github.com/damian-pastorini/game-data-generator/blob/master/lib/generator/attributes-per-level.js

Require parameters:
- "templateBase": this will be the starting point for each "stat" value.
- "typeTemplates": these will be your "class paths" keys, for each class path, the generator will create all the "stats" values per "level".
- "typesVariations": similar to the type templates but in this case is to generate a variation value using a minimum and a maximum amount.
- "maxLevel": if not specified then 100 will be used as default.

To use the generator follow these steps:

- Go to your game folder and create a folder called "generate-data".
- Inside the created folder create a new file named "attributes-per-level.json".
- Save the following content in the file:
```
{
    "templateBase": {
        "hp": 20,
        "mp": 20,
        "atk": 10,
        "def": 10
    },
    "typeTemplates": {
        "Mage": {
            "hp": 25,
            "mp": 40,
            "atk": 12,
            "def": 12
        },
        "Warrior": {
            "hp": 40,
            "mp": 20,
            "atk": 25,
            "def": 22
        }
    },
    "typesVariations": {
        "player": {
            "min": 1,
            "max": 2
        }
    },
    "typeScaleFactorRandom": 0.6
}
```
This JSON contains the parameters that will be passed to the `attributes-per-level` command.

- Open a console for the command line in your game folder.
- Run the following command:
```
$ npx reldens-generate attributes-per-level ./generate-data/attributes-per-level.json
```
- As result, a new folder called "generated" will be created under your "game" folder, and there you will find a file with the generated data like:
```
{
    "statsByVariation": {
        "player": {
            "1": {
                "Mage": {
                    "hp": 123,
                    "mp": 176,
                    "atk": 39,
                    "def": 39
                },
                "Warrior": {
                    "hp": 176,
                    "mp": 106,
                    "atk": 62,
                    "def": 56
                }
            },
            "2": {
                "Mage": {
                    "hp": 134,
                    "mp": 192,
                    "atk": 42,
                    "def": 42
                },
                "Warrior": {
                    "hp": 192,
                    "mp": 115,
                    "atk": 67,
                    "def": 61
                }
            },
....
```
