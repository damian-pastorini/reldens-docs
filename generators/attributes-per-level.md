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
```json
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
```json
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

In the example above we are generating the attributes for the player class paths, but in the same way we could easily use it to generate the enemies attributes per level and later assign these attributes for different monsters to increase the difficulty over the levels.

For example, we can use the following configuration ([see sample file here](../examples/generate-data/attributes-per-level-enemies.json)):

```json
{
    "templateBase": {
        "hp": 10,
        "mp": 10,
        "atk": 10,
        "def": 10,
        "speed": 10,
        "mAtk": 10,
        "mDef": 10,
        "dodge": 10,
        "aim": 10
    },
    "typeTemplates": {
        "melee": {
            "hp": {"min": 10, "max": 20},
            "mp": {"min": 1, "max": 5 },
            "atk": {"min": 10, "max": 20},
            "def": {"min": 10, "max": 20},
            "speed": {"min": 1, "max": 2},
            "mAtk": {"min": 1, "max": 2},
            "mDef": {"min": 1, "max": 2},
            "dodge": {"min": 1, "max": 4},
            "aim": {"min": 1, "max": 2}
        },
        "mage": {
            "hp": {"min": 5, "max": 10},
            "mp": {"min": 10, "max": 20},
            "atk": {"min": 1, "max": 2},
            "def": {"min": 1, "max": 2},
            "speed": {"min": 1, "max": 4},
            "mAtk": {"min": 10, "max": 20},
            "mDef": {"min": 10, "max": 20},
            "dodge": {"min": 1, "max": 2},
            "aim": {"min": 5, "max": 10}
        },
        "archer": {
            "hp": {"min": 5, "max": 10},
            "mp": {"min": 5, "max": 10},
            "atk": {"min": 5, "max": 10},
            "def": {"min": 1, "max": 4},
            "speed": {"min": 5, "max": 10},
            "mAtk": {"min": 1, "max": 2},
            "mDef": {"min": 1, "max": 2},
            "dodge": {"min": 7, "max": 20},
            "aim": {"min": 7, "max": 20}
        }
    },
    "typesVariations": {
        "monsterA": {
            "min": 1,
            "max": 1.5
        },
        "monsterB": {
            "min": 1.5,
            "max": 1.8
        },
        "boss": {
            "min": 2.5,
            "max": 3.5
        }
    }
}
```

With these you will get a file like: [monsters-attributes-per-level-generated.json](../examples/generated/monsters-attributes-per-level-generated.json)
```
{
    "statsByVariation": {
        "monsterA": {
            "1": {
                "melee": {
                    "hp": 47,
                    "mp": 16,
                    "atk": 45,
                    "def": 43,
                    "speed": 16,
                    "mAtk": 16,
                    "mDef": 16,
                    "dodge": 16,
                    "aim": 17
                },
                "mage": {
                    "hp": 29,
                    "mp": 48,
                    "atk": 17,
                    "def": 17,
                    "speed": 17,
                    "mAtk": 45,
                    "mDef": 47,
                    "dodge": 16,
                    "aim": 31
                },
                "archer": {
                    "hp": 26,
                    "mp": 26,
                    "atk": 31,
                    "def": 16,
                    "speed": 30,
                    "mAtk": 17,
                    "mDef": 17,
                    "dodge": 43,
                    "aim": 44
                }
            }
//...
```

You can use the "keys": "monsterA", "monsterB" and "boss", on the "objects" for the "Objects Importer", to create the objects "stats".

By passing the generated file like in the example below:
```
{
    "objects": [
        {
            "clientKey": "rat",
            "title": "Bad Rat",
            "layer": "ground-respawn-area-level-1",
            "level": "1",
            "experienceKey": "monsterA",
            "attributesKey": "monsterA",
            "attributesSubTypeKey": "melee",
            "privateParams": {
                "interactionRadio": 60
            },
            "clientParams": {
                "autoStart": true,
                "frameStart": 0,
                "frameEnd": 2,
                "repeat": -1
            },
            "assets": [
                {
                    "assetKey": "rat",
                    "assetFile": "level-001-rat-108x136-36x34.png",
                    "extraParams": {
                        "frameWidth": 36,
                        "frameHeight": 34
                    }
                }
            ]
        }
        // ...
    ],
    // ...
    "attributesPerLevelFile": "monsters-attributes-per-level-generated.json"
```

The `attributesKey` and the `level` in the "object" will automatically use the data from the file (`statsByVariation[attributesKey][level]`) to create each the object "stats".

