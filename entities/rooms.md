### Rooms

The basic function for any room is to handle the communications and share the information between all the players in the room.

In Reldens you will find different types of rooms. 

- RoomLogin: is kind of an abstract room that provides the user authentication system and almost every room extends from this one.
- RoomScene: this type of room is always related to a "scene" or "map", and a world instance will be created for this room based on the map data provided.
