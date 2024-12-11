## Customize your game

### How to apply your customizations

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

