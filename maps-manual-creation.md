## How to create a new Room/Scene?

This section will describe all the tools and the process to create a new Scene from scratch.

### Recommended tools

- Tiled Map Editor: https://www.mapeditor.org
- Tiled Map Optimizer: https://www.reldens.com/tiled-map-optimizer/
- Tile Map Generator: https://www.reldens.com/documentation/tile-map-generator > https://github.com/damian-pastorini/tile-map-generator/
- Frame Extruder: https://github.com/lgibson02/FrameExtruder

### Create the map

Open the Tiled Map Editor app and create a new map with a fixed size (for example 30 x 30).

The most IMPORTANT considerations here are:

- "How you split the map layers": since this will affect if the layers go over or below the player sprint.
- "The map layers name conventions": this way Reldens will identify which layers are used for the collisions, the scene change-points, the return points, the respawn areas, and every other map behavior like how the layers will be displayed according to the player. For last, the layers name conventions are used for both server and client sides.

Layers name conventions:

#### "collisions"

Any layer with this keyword in the name will be used to create blocks used for collisions in the server side. A collision in the server side will be represented by a empty box with the size of a tile, so if you edit your map and hit/collide with an empty space, is probably because you have a tile with a value different from zero in that position in a layer with the word "collisions" on the name.

To avoid this kind of issues I recommend you to use the TiledMap option to "Highlight Current Layer" (available pressing H while editing the map), this way you will easily see if there's any non-empty blocks in any "collision" layer.

#### "over-player"
Any layer with this keyword in the name will get an incremental depth in the client side, this way the map view will be affected by the layers order in the file and by the layers name that will get the incremental depth, so even when you can see the layers properly displayed in the TiledMap editor you may not get the exact same result after we process the layers to all these over the player.

For example: if you have 5 layers, and the 3rd and 5th in the list have "over-player" in the name, the layers will get the following depth in Phaser: L1 = depth 0, L2 = depth 0, L3 = depth 1, L4 = depth 0, L5 = depth 2 > where the player sprite will have depth 0 and go over all the other layers, the L3 and 5 will be over the player.

#### "change-points"
Any layer with this in the name should only have tiles are going to be used as change-points in the server side.

At this time if you used multiple images to create your maps, you will need to merge them in one, for that you can check optimize steps below.

#### "respawn-area"
The layers that starts with this keyword will be used for the respawn objects areas and though this layers requires to have content on them to know the valid tiles for respawn, these will never generate collisions.
