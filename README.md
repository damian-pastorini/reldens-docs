# Reldens - Documentation

Version: 4.0.0

Project GitHub: https://github.com/damian-pastorini/reldens

Website: https://www.reldens.com/

Join us on Discord: https://discord.gg/HuJMxUY

Follow the project progress in the GitHub board: https://github.com/users/damian-pastorini/projects/2/views/1

---

## Sample game creation process:

### - Step #1 - Installation

Install Reldens following the [installation guide](https://github.com/damian-pastorini/reldens-docs/blob/master/installation.md).

### - Step #2 - Contents creation

The minimum required contents are related between each other, so you need to create them in the following order:

- [Stats](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/stats.md)
- [Level Sets](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/levels-set.md)
- [Class Paths](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/class-path.md)
- [Levels](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/level.md)
- [Levels Modifiers](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/level-modifiers.md)
- [Skill Types](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/skill-types.md)
- [Skills](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/skill.md)
- [Rooms](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/rooms.md)
- [Objects](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/objects.md)
- [Respawn Areas](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/respawn-areas.md)

Note: though is recommended to learn the info in the links above, you don't need to read all of them now to follow the content creation steps.

Ways to create the game contents:
- Through the [generators and imports](https://github.com/damian-pastorini/reldens-docs/blob/master/generators-and-imports.md) available as commands.
- Through the generators and imports available in the [administration panel](https://github.com/damian-pastorini/reldens-docs/blob/master/administration-panel.md).
- Manually creating each entity in the administration panel.
- Directly with queries in the database using any client (not recommended).

---

First we will use the generators available on the commands to get as much data as possible to later process with the importers.

- Use the [players experience generator](https://github.com/damian-pastorini/reldens-docs/blob/master/generators/players-experience-per-level.md) to create the players experience data file or use the [example file /examples/generate-data/players-experience-per-level.json](https://github.com/damian-pastorini/reldens-docs/blob/master/examples/generate-data/players-experience-per-level.json).
- Copy the resulting file from the "generated" folder into the "generate-data" folder and rename it to `class-paths.json`.
- In that file (`class-paths.json`) we will include our classes paths information.
- For the documentation we will create 2 classes: "Warrior" and "Mage", you can create as many as you like, but 1 is required for the platform to work (even when later you don't show it anywhere in the game).
- As you can see in the example below we are also including different "labels" for the paths at different levels (50 and 100), this will represent our class paths changes (with code you could customize the behavior to make the players change classes through an NPC).
- Additionally, in the same file we will include another parameter called "preAppendRace" = true, which will be used by the importer later.
- Your class-paths file should look [like this /examples/generated/class-paths.json](https://github.com/damian-pastorini/reldens-docs/blob/master/examples/generated/class-paths.json):
```
{
    "preAppendRace": true,
    "classPaths": {
        "Mage": {
            "50": "Wizard",
            "100": "Sage"
        },
        "Warrior": {
            "50": "Guardian",
            "100": "Warlord"
        }
   },
   "levelsSets": {
        "all": {
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
            // here you should put the generated levels data
        }
    }
}
```
- Use the [attributes per level generator](https://github.com/damian-pastorini/reldens-docs/blob/master/generators/attributes-per-level.md) to create the "stats" with their incremental values per level for each of your classes or use this [example file /examples/generate-data/attributes-per-level](https://github.com/damian-pastorini/reldens-docs/blob/master/examples/generate-data/attributes-per-level.json). 
