### Objects

An "Object" in Reldens can be almost anything: from static things in a map, moving things with animations, NPCs, enemies, etc. 

Here's a brief description on each available object types by default:

- `base`: this object contains the basic functionality of every object in the game (all the other types extends from this one), it only handles the mapping for the private and client properties.
- `animation`: this type only includes the object movement as feature, it can be activated automatically through the `autoStart`, `onHit` or `onAction` and it can chase other bodies.
- `npc`: this type follows the `animation` type but includes messages and interactions handling through options. 
- `enemy`: this type will have a `physics body` and `stats` to be able to fight with players, can be aggressive or not, can have skills, start battles, etc.
- `trader`: this type implements the specific trade behavior which is pretty complex.
- `multiple`: this type will create multiple instances of the same specified child-type (normally used on respawn areas).
- `drop`: this type will normally represent an [item entity](item.md) that would have a body so it can be picked up on hit or by interacting with it. 
