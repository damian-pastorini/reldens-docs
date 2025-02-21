## Customize your game

The first recommendation I'm going to write here is not related to the platform but to your game creation plan:
is highly important that you have ready as many assets as you can.

Customize your game means you will modify the platform to implement your game flow, the layout, all the main elements like maps, objects, players, animations, etc. For all this you will need all the related graphics ready to be implemented.

One way to make sure you have everything, could be to go through all the elements that are used in the default theme, since there you will find how many assets you need.
For example, here you can find a basic list:
- Your game fonts (are you going to use some web font, or a custom one embed on your game?).
- Your game logo.
- A homepage design, let's say with a background.
- Does your game layout contain custom elements like fancy images for borders or boxes backgrounds? Get those images ready as well.
- The styles sheets related if you bought some kind of game "theme".
- You will need icons: not only for the game layout (like for controls or settings buttons), but also for stuff like weapons and items that will be displayed in the inventory.
- Get ready your sprites for every [player class path](assets/player-sprite.md), for every [object / NPC / enemy](assets/object-sprite.md).
- You need your players and enemies [skills animations](assets/skill-sprite.md).
- Probably I've implied this on the previous step of the game creation: you should have all your maps tilesheet ready. And if you are going to use the map wizard you better have all your [maps elements](generators/maps-elements.md) or [composite files](generators/map-composite-file.md) as well.

As you can see all of this is TON of contents and better you be ready.


### - How to apply your customizations

Since Reldens gives you both sides of a game, server and client, some customizations will require a server reboot and some will additionally require a client rebuild before the reboot.

- To reboot the game server (for now), you will need to kill the node process and start it again.

- To rebuild the client you will need to run the following commands according to your needs:

```
$ npx reldens help

$ npx reldens copyAssetsToDist [your-game-theme-folder]

$ npx reldens buildCss [your-game-theme-folder]

$ npx reldens buildClient [your-game-theme-folder]
```

With these commands in mind we can now start customizing the game.

### - Changing the registration and login options

Through the admin panel we can modify the following parameters (filter by `path`):

- `general/users/allowRegistration`: enable / disable default registration process.
- `general/users/allowGuest`: true by default, enable / disable the guest login.
- `players/guestUser/allowOnRooms`: true by default, if guest users are enabled then you can limit the rooms the guest players can access, this requires to add `"allowGuest":true` in the room custom data (edit room in the admin). 
- `players/multiplePlayers/enabled`: this will allow users to create more than one player on their accounts.
- `rooms/selection/allowOnLogin`: enabled / disable the room selection on login, since you can specify the serverUrl in the room custom data, this can be used for players server-selection.
- `rooms/selection/allowOnRegistration`: enabled / disable the room selection on registration, since you can specify the serverUrl in the room custom data, this can be used as one time server-selection.

NOTE: though every change can be done in the admin, a good recommendation here is to actually save all these updates as queries, that way you will be always able to track your game config changes and reset your entire server or deploy new database instances easier.  


### - Enabling guest users on recently generated rooms

By default, the generated rooms will not have the "allowGuests" option in their custom data.

If you enabled the guest login, you will need to update the rooms with the parameter, for that you can:
- Update the rooms manually through the admin (if you need to do it in some rooms will be easier).
- Update the rooms with a query if you need to do it for too many rooms:
```sql
UPDATE `rooms`
SET 
    `customData` = CASE
        WHEN JSON_VALID(`customData`) THEN JSON_SET(`customData`, '$.allowGuest', TRUE)
        ELSE '{"allowGuest":true}'
    END
-- here you can filter by the rooms you need:
-- WHERE `id` = IN ([your ids]) OR `name` LIKE '%some part of the room name%'
;
```

### - Customize your theme

Start by removing the disclaimer message from: `[your-game-folder]/theme/[your-theme-name]/index.html`.

Search "row-disclaimer" and delete the entire block.

Now edit the index.js file from the same folder: `[your-game-folder]/theme/[your-theme-name]/index.js`.

Remove this entire block:
```js
// demo message removal:
reldens.events.on('reldens.startGameAfter', () => {
    reldens.gameDom.getElement('.row-disclaimer')?.remove();
});
```

For last remove the styles from the base.scss file: `[your-game-folder]/theme/[your-theme-name]/css/base.scss`.

Remove this entire block:
```scss
.disclaimer {
    text-align: center;
    max-width: 80%;
    margin: 0 auto;
    padding: 10px 2%;
    background-color: rgba(255,255,255,0.1);
}
```

You can also remove the version block:
```js
// client event listener example with version display:
reldens.events.on('reldens.afterInitEngineAndStartGame', () => {
    reldens.gameDom.getElement('#current-version').innerHTML = reldens.config.client.gameEngine.version+' -';
});
```

Then at the top of the file you will see the log level been set, you can change it as you like, for example to avoid the change by query parameter. 
```js
const urlParams = new URLSearchParams(window.location.search);
window.RELDENS_LOG_LEVEL = (urlParams.get('logLevel') || 7);
window.RELDENS_ENABLE_TRACE_FOR = Number(urlParams.get('traceFor') || 'emergency,alert,critical');
```

I normally leave this block over the development process and remove it before publish the game since it's handy to quickly debug stuff.

In that same file you can see how the skills cold down works, if you don't want to use that you can remove it as well.

Next: remove the extra languages if you don't need them, from the sample data you can remove:
- `[your-game-folder]/theme/[your-theme-name]/es-index.html`

Next we need to tackle a known bug: 
- `[Know bug v4.0.0-beta.38.3]` - Remove unused default theme assets.

These are the files that can be safely removed (some are used as default and must be replaced by your own):
- `[your-game-folder]/theme/[your-theme-name]/assets/audio/footstep.mp3`
- `[your-game-folder]/theme/[your-theme-name]/assets/audio/reldens-town.mp3`
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/actions/controls/*`
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/actions/sprites/fireball*`
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/actions/sprites/heal*`
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/groups/*`
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/items/*`
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/rewards/*`
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/sprites/*` except `player-base.png`, `warrior.png` and `mage.png` (these two are because the created class paths following the sample).
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/maps/reldens*` since every map generated does not have `reldens` as name all of these are actually from the sample data and can be removed as well.

Update your game favicons which are located in:
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/favicons`

Update your game logo and game background (if needed), the files are located in:
- `[your-game-folder]/theme/[your-theme-name]/assets/custom/web/`
And after change the files then you can change the logo file name in the index and the game layout templates:
- `[your-game-folder]/theme/[your-theme-name]/index.html`
- `[your-game-folder]/theme/[your-theme-name]/assets/html/layout.html`
Search for "your-logo", and replace the image name in that block:
```html
<img id="your-logo" src="./assets/web/reldens-your-logo-mage.png" alt="reldens"/>
```
The background has to be replaced in the styles file:
- `[your-game-folder]/theme/[your-theme-name]/css/base.scss`
Search for `.wrapper`, and change the style:
```scss
.wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-height: 100%;
    overflow: auto;
    z-index: 10000;
    background-size: cover;
    background-color: $cWhite;
    background-image: url(../assets/web/reldens-background.png);
    background-position: center;
    background-repeat: no-repeat;
}
```
