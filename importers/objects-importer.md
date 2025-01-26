## Objects Importer

The way the objects importer works is with a JSON file that should contain the complete objects data but with some extra
benefits, like:

- Having a "defaults" data set.
- Getting the related respawn areas automatically created.

**IMPORTANT**: the importer will create all the objects related records, but you will have to manually upload the assets files to the proper folder `[your-theme-folder]/assets/custom/sprites/`. 

```
{
    "objects": [
        {
            "clientKey": "bat",
            "title": "Bad Bat",
            "layer": "ground-respawn-area-level-1",
            "level": "1",
            "experienceKey": "monsterA",
            "attributesKey": "monsterA",
            "attributesSubTypeKey": "melee",
            "privateParams": {
                "shouldRespawn": true,
                "childObjectType": "enemy",
                "isAggressive": true,
                "interactionRadio": 120
            },
            "clientParams": {
                "autoStart": true,
                "frameStart": 0,
                "frameEnd": 2,
                "repeat": -1
            },
            "assets": [
                {
                    "assetKey": "bat",
                    "assetFile": "bat-270x384-90x96.png",
                    "extraParams": {
                        "frameWidth": 90,
                        "frameHeight": 96
                    }
                }
            ]
        },
        {
            "clientKey": "bear_brown",
            "title": "Hungry Bear",
            "layer": "ground-respawn-area-level-2",
            "level": "1",
            "experienceKey": "monsterB",
            "attributesKey": "monsterB",
            "attributesSubTypeKey": "melee",
            "privateParams": {
                "shouldRespawn": true,
                "childObjectType": "enemy",
                "isAggressive": true,
                "interactionRadio": 70
            },
            "assets": [
                {
                    "assetKey": "bear_brown",
                    "assetFile": "bear-brown-165x152-55x38.png",
                    "extraParams": {
                        "frameWidth": 55,
                        "frameHeight": 38
                    }
                }
            ]
        }
    ],
    "defaults": {
        "classType": "multiple",
        "enabled": 1,
        "animations": {
            "up": {
                "start": 9,
                "end": 11
            },
            "down": {
                "start": 0,
                "end": 2
            },
            "left": {
                "start": 3,
                "end": 5
            },
            "right": {
                "start": 6,
                "end": 8
            }
        },
        "respawn": {
            "respawnTime": 2000,
            "instancesLimit": 4
        },
        "roomsNames": [
            "boots-001",
            "boots-002",
            "boots-003"
        ]
    },
    "attributesPerLevelFile": "monsters-attributes-per-level-generated.json",
    "experiencePerLevelFile": "monsters-experience-per-level-generated.json"
}
```

The importer will loop over each "object" and create a data set that will clone the "defaults" to use these as base.
It will do a deep clone on the "defaults" and a deep merge on each property, meaning, if your "defaults" looks like this:
```
defaults: {
    property: {
        existentPropertyB
    }
}
```
And the current object has a value like:
`currentObject.property.subPropertyA = 'asdasd'`
This will override or be included a part of the existent `property` in the defaults, like:
```
defaults: {
    property: {
        existentPropertyB: 'qweqwe',
        subPropertyA: 'asdasd'
    }
}
```

In order to complete the objects crete we need to know the room ID for that object. 
Since manually writing the room IDs would be difficult and unclear to which room the object is going to be assigned, here we can use the `roomsNames`.
The importer will fetch the rooms IDs and create one `object` per each specified room here.
In the case above the 2 objects are going to be created in 3 rooms.

As you can see in the example above, we also need to know the `layer` (`layer_name` in the storage).
The specified layer is also used to create the respawn area for the object.

### Objects animations:
For now, Objects has 2 places where we need to define the animations:
- The "default" animation, which is defined in the `object.clientParams` and passed as part of the object properties.
- All the other animations defined by a name convention in the `animationKey` coming from the storage.

**IMPORTANT**: the `animationKey` convention follows the format `[layer-name]_[object-ID]_[key]`, where `key` is the part of the convention to set the animation `direction`.

For example, following the JSON above, you would get entries with the following keys for the first object:
```
ground-respawn-area-level-1_60_up
ground-respawn-area-level-1_60_down
ground-respawn-area-level-1_60_left
ground-respawn-area-level-1_60_right
```
