### Level Modifiers

A "level modifier" in Reldens is a way to establish the player "stats" increments by level.

For example:
- In level 1 the player will have 20 "HP".
- In level 2 that will be incremented 10 (30 HP in total). 

To make that happen we need to create a "level modifier" for the "level 2" (related by level ID) that will have a "value" of 10 for the player "HP" property.

Though we will always have a "single" set of "stats", the entities (like players or NPCs), will have two sets of the same "stats":
- The "stats" itself that will contain the current value of the stat.
- The "statsBase" that will contain the "maximum" value for the stat.

An easy example of this is the common "HP" or "MP" that will be normally increase/decrease with damage or magic, and where you still need to keep the original maximum value like:
- HP 20 / 100
- MP 83 / 100
- [property] [stat-current-value] / [stat-base-value]

These two keys ("stats" and "statsBase") are "hardcoded" in the entities and all over the game logic.

In order to create a modifier we need to specify:
- "level owner": relation by level ID.
- "key": a string to identify the modifier.
- "property key": the path to the property including the initial "set", like "stats/hp" or "statsBase/hp".
- "operation": normally will be "increment", but you can set any of the available [operations](general/operations.md)
- "value": the value that will be applied according the selected "operation".
 
Note, operations can be used to reduce a "stat" if let's say you want your player change their "path" goal. For example: learning magic will increase the "MP" but at the same time could reduce a player "strength".

