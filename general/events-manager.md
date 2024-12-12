## Events Manager

When you create a new ServerManager or GameManager (client-side) the EventsManagerSingleton is automatically assigned to that manager so you can use it for any listener you like.

This way you will be able to listen to all the platform events and modify the server or the client behaviors without requiring to modify the core code.

In the skeleton example you will find the server manager initialization in the index file:

https://github.com/damian-pastorini/reldens-skeleton/blob/master/index.js

Here you can see that you only need to access the ServerManager.events property (which is the EventsManagerSingleton instance), and append your event, that's it!

The same applies for the GameManager on the client side:

https://github.com/damian-pastorini/reldens-skeleton/blob/master/theme/custom-game-theme-test/index.js

The EventsManager is an extension of the AwaitEventEmitter, which by default allow us to use sync and async events. In our case we extended it a bit further to include some extra features:

- The main addition are the "removeKey" and the "masterKey", you can specify these while adding an event listener and that listener will be associated to an specific "group" under those keys, this way you can turn off multiple events at once using any of the keys.
- The second is the debug mode that will generate logs for every listener added and every time an event is fired. This debug mode can be set using the EventsManager.debug property, and it can be configured as "all" (for every event), or for specific events (see debug configuration below).

### - Types of events

Since we are working with a multiplayer platform in the server side we have different event types.

What does this mean? It means that some events are going to be executed "globally" and some are going to use keys for specific rooms, players or objects.

We need to differentiate these because the EventsManager is a singleton. This design allows us to easily use it anywhere in the system.

However, it also means that every single event will be fired globally. To address this, we created specific event keys. Without these keys, you would have to apply numerous filters on each listener to ensure that the event was triggered for a specific room, player, or object.

For example:
- The event "reldens.beforeLoadConfigurations" is going to be executed globally (and for now, only once) when the server is initialized.
- But also you can find events with dynamic keys like in the skills package:
  "p+[player-id]+.reldens.items.equipItem" => "p1.reldens.items.equipItem"

Which is designed to affect only the player with id = 1.

This was designed this way because, without applying a key, the server would trigger the event "reldens.items.equipItem" globally. This would require you to manually send and validate which player the item was equipped for.

### - IMPORTANT, setting events off:

For every event listener you create you must set that event off when the player leaves the room, when the object is destroyed or when the room gets disposed.

IMPORTANT: if you don't it properly the events may keep references to the entities (players, objects or rooms), and by that those elements won't be valid for the garbage collector which could end in memory leaks.


### Available events

In order see ALL the available events in Reldens, you can simply search on the library file for every string like `'reldens.`, every event name in Reldens starts with the same string.

But here you can check the most "used" events with the recommendation:

- `reldens.preloadUiScene`: for when you need to load custom assets.
- `reldens.createPreload`: this can be used when you need to include custom animations.
- `reldens.createUiScene`: to include custom elements on the game layout.
- `reldens.roomsMessageActionsGlobal`: this allows you to include custom global room messages listeners.  
- `reldens.roomsMessageActionsByRoom`: same as before but per/room.
- `reldens.beforeSuperInitialGameData`: this can be used for example to add custom player data when the initial data is sent to the user.
- `reldens.createdPlayerSchema`: this can be used to enrich the player entity right after it was created.
- `reldens.joinedRoom`: ideal to add messages listeners on the client side.
- `reldens.roomsDefinition`: can be used to include custom rooms in the rooms list.
- `reldens.battleEnded`: this can be used to execute custom actions when a battle ends (player or NPC dies, player scape, etc. this is triggered by multiple causes).
- `reldens.playerDeath`: similar to battleEnded but limited to when a player dies.
- `reldens.gameEngineShowTarget`: ideal for when you need to modify the target view block.

And many more, but we will continue adding to the list according to use.
