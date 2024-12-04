### Stats

The "stats" in Reldens are the player "properties" that will be used for the game logic, for now, on the skills and battle system.

By default, on each [Skill](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/skill.md) you can specify to which behavior the property is related: attack, defense, aim or dodge.
These are temporally "hardcoded" behaviors but could be customized with code to change the logic on how it works.

Beside in each skill we also have a more "general" options through the [System Configuration](https://github.com/damian-pastorini/reldens-docs/blob/master/configuration.md), where we can set the following "scope"/"paths":
- "actions/skills/affectedProperty": the property that is going to be used to apply the "calculated damage".
- "enemies/default/affectedProperty": same as the previous one but for the enemies (NPC).
- "ui/clan/sharedProperties": the properties that will be shared between players in the same clan.
- "ui/teams/sharedProperties": the properties that will be shared between players in the same team.
- "players/physicsBody/usePlayerSpeedProperty": if you create a property called "speed" you can tell here if you like to use it to change the player body speed making it move slower or faster according to the "speed" property value.
- "enemies/initialStats/[stat-key]": these are the properties and default values assigned to the enemies.
