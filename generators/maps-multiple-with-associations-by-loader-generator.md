## Generate multiple maps with associations by loader generator

This option is a reference to the `MultipleWithAssociationsByLoaderGenerator` class from the `@reldens/tile-map-generator` package.

This generator reuse the `LayerElementsCompositeLoader` to get all the elements from a single map file and then again from the nested associated maps.

Sample parameters:

```json
{
    "factor": 2,
    "mainPathSize": 3,
    "blockMapBorder": true,
    "freeSpaceTilesQuantity": 2,
    "variableTilesPercentage": 15,
    "collisionLayersForPaths": [
        "change-points",
        "collisions",
        "tree-base"
    ],
    "mapsInformation": [
        {
            "mapName": "town-001",
            "mapTitle": "Town 1"
        },
        {
            "mapName": "town-002",
            "mapTitle": "Town 2"
        },
        {
            "mapName": "town-003",
            "mapTitle": "Town 3"
        },
        {
            "mapName": "town-004",
            "mapTitle": "Town 4"
        }
    ],
    "associationsProperties": {
        "generateElementsPath": false,
        "blockMapBorder": true,
        "freeSpaceTilesQuantity": 0,
        "variableTilesPercentage": 0,
        "placeElementsOrder": "inOrder",
        "orderElementsBySize": false,
        "randomizeQuantities": true,
        "applySurroundingPathTiles": false,
        "automaticallyExtrudeMaps": true
    },
    "compositeElementsFile": "reldens-town-composite-with-associations.json",
    "automaticallyExtrudeMaps": "1"
}
```

Parameters description:

- "factor": This is the value used to increase / decrease the map images size. For example, if your map is 16x16, but you need it to be 32x32, you can set a "2" to multiply the image size. 
- "mainPathSize": The main path size is the amount of tiles used to start the map in the borders.
- "blockMapBorder": This would make the map border tiles walkable or not.
- "freeSpaceTilesQuantity": The amount of tiles between the map elements.
- "variableTilesPercentage": The percentage of the total map that will be used to place random ground tiles from the specified variations.
- "collisionLayersForPaths": An array of layers that will not allow the generator to create the path over.
- "mapsInformation": An array of maps data objects containing the "mapName" and the "mapTitle" to be generated.
- "associationsProperties": The object that will contain the sub-maps generation options. Since this is a sub-call for the same generator, here you can find the same options as for the main map but with different values.
  - "generateElementsPath": This will avoid the path creation inside the sub-maps.
  - "blockMapBorder"
  - "freeSpaceTilesQuantity"
  - "variableTilesPercentage"
  - "placeElementsOrder": The default value here is "random", but "inOrder" will make the generator place one element after the other in the map.
  - "orderElementsBySize": This will make the generator to order the elements according to their biggest layer.
  - "randomizeQuantities": This will randomize the entire elements array, for example 2 houses, 2 trees, could get 1 tree, 2 houses, 1 tree, or house, tree, house, tree, etc.
  - "applySurroundingPathTiles": This option is true by default, it will make the generator look for the path corners tiles and apply those to the main path, this way you can get paths with rounder corners.
  - "automaticallyExtrudeMaps": This option is true by default, this will prevent tile bleeding issues.
- "compositeElementsFile": This is a reference to the uploaded JSON file used for the sub-maps data.
- "automaticallyExtrudeMaps": This is to prevent tile bleeding issues on the main maps.
