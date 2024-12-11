## Customize your game

### - How to apply your customizations

Since Reldens gives you both sides of a game, server and client, some customizations will require a server reboot and some will require a client rebuild and the server reboot.

- To reboot the game server (for now), you will need to kill the node process and start it again.

- To rebuild the client you will need to run the following commands according to your needs:

```
$ npx reldens help

$ npx reldens buildCss [your-game-theme-folder]

$ npx reldens buildClient [your-game-theme-folder]

$ npx reldens copyAssetsToDist [your-game-theme-folder]
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
