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

The layer deep will be calculated like: layer index * map.height * map.tileHeight.

#### "change-points"
Any layer with this in the name should only have tiles are going to be used as change-points in the server side.

At this time if you used multiple images to create your maps, you will need to merge them in one, for that you can check optimize steps below.

#### "respawn-area"
The layers contain this keyword in the name, the layer will be used for the related respawn object areas and every tile different from `0` in this layer will be used for respawn objects. 

Note: when creating these respawn areas you don't need to worry about the "non-walkable" tiles since Reldens will filter those when the respawn area is created, meaning you could set a fully occupied layer as your tile map base and still get objects only respawning in the "free" tiles. 

#### "below-player"

### Add multiple tilesets to the same map

If your map has more than one tileset you need to include multiple scene images and each tileset name in the `JSON` must have the same name as the image without the file extension.

First you need to edit you `room` and upload multiple images for the "Scene Images", for example:

![Multiple scene images](./screenshots/maps-creation-multiple-images.png)

Then edit your map `JSON` file, search for the "tilesets", and fix their names after their image file names like:

```
"image":"reldens-forest.png",
"name":"reldens-forest",
```

```
// ... 
"tilesets": [
    {
        "columns":14,
        "firstgid":1,
        "image":"reldens-forest.png",
        "imageheight":408,
        "imagewidth":476,
        "margin":1,
        "name":"reldens-forest",
        "spacing":2,
        "tilecount":168,
        "tileheight":32
    }
// ...
```

- `[Know bug v4.0.0-beta.38.3]` - Multiple images here is breaking because all the tilesets are been included with the same key and the tileset key must be unique.
