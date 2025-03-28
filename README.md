# ClassBoom Saving
This is a hafly open source project. Here there are possibilities to modify the saving files to get, the results, that are not possible in the base game.

Here will be described how this format works and how to add your additions.
## The file format

The .cbd file format is for saving Class Boom Saves. It is based on JSON. Here every file starts with:
- version - the version of the game (string)

### Tilemap

Then there is a long tilemap data, which is one big array of a tile data, that includes:
- x - horizontal position
- y - vertical position
- t - type of the tile (there is only 0 for now)


### Objects
Here comes the interesting parts. The objects in the game

Here are all the parts:
- index - doesn't change anything, but must be unique

- name - the name of the object (does nothing)

- transform - an array, that represents x position, y position, rotation, x scale, y scale

- rigidBodyData - an array, that represents mass, gravity, drag

- constrains - a number, that locks an axis or rotation: here is the table:

|              | Position X |  Position Y  | Rotation |
|--------------|------------|--------------|----------|
| Position X   | 1          | 3            | 5        |
| Position Y   | 3          | 2            | 6        | 
| Rotation     | 5          | 6            | 4        |

To lock all constrains put 7

- material - an array of 2 values, that are friction and bounciness.

- look - the shape and the texture of the object
    
    - shape - a shape of the object (1 - box, 2 - circle, 3 - triangle).

    - texture - a string, that represents a texture:


![Textures](https://raw.githubusercontent.com/R0fael/ClassBoom-Saving/refs/heads/main/resources/names.png)

- sound - an array of two sounds(or effects), that are for collision and destruction(explosion or glass). Available sounds are: Bouncy, Explosion, Glass, Ice, Sand, Soft, Touch

- isSilent - means if doesn't has a collision sound

- gluedObjects - an array of objects' id, that are glued to that object.

#### Components

Every object have components, that add behaviours to the object. Every component has "enabled" value, that enables or disables the component


- explosions - a component, that allows the object to explode.

    - force - the force of the dinamite
    - radius - the radius of impact
    - time - the time before the object exolodes
    - offset - a randomized offset of time.


- boosterData - makes a brust on click

    - xForce - horizontal force
    - yForce - vertical force
    - isGlobal - will make the booster force point to same direction in the world or else it will be changed with the rotation

- glassData - destroys on collision
- glueData - glues other objects together

### Ropes

This section is only for rope connections. It is made out of ropes, that are compound of:

- object1 - index of the first connection
- object2 - index of the second connection
- distance - the distance of the rope
- width - the width of the rope
- dampingRatio - the dampingRatio of the rope
- frequency - the strength of the rope


## Examples

Here I will show some examples of modified worlds.

### Developer World
A minimalistic world. Easier to modify

```json
{
    "version": "0.3",
    "tilemap": [
        {"t": 0, "x": -2, "y": -5},
        {"t": 0, "x": -1, "y": -5},
	{"t": 0, "x": 0, "y": -5},
        {"t": 0, "x": 1, "y": -5}
    ],
    "objects": 
    [
        {
            "index": 100,
            "name": "Object",
            "transform": [
		0.0,
		0.0,
		0.0,
                1.0,
                1.0
            ],
            "rigidBodyData": [1.0, 1.0, 0],
            "constrains": 0,
            "material": [0.4,0.0],
            "look": {"shape": 1,"texture": "white_square"},
            "sounds": [6,4],
            "isSilent": false,
            "gluedObjects": [],
            "explosions": {
                "enabled": false,
                "force": 0.0,
                "radius": 0.0,
                "time": 0.0,
                "offset": 0.0
            },
            "boosterData": {
                "enabled": false,
                "xForce": 0.0,
                "yForce": 0.0,
                "isGlobal": false
            },
            "glassData": {"enabled": false},
            "glueData": {"enabled": false}
        }
    ],
    "ropes": [
        {
            "object1": 0,
            "object2": 0,
            "distance": 1,
            "width": 0.1,
            "dampingRatio": 0.0,
            "frequency": 1.0
        }
    ]
}
```
