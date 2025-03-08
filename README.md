# ClassBoom Saving
This is a hafly open source project. Here there are possibilities to modify the saving files to get, the results, that are not possible in the base game.

Here will be described how this format works and how to add your additions.
## The file format

The .cbd file format is for saving Class Boom Saves. It is based on JSON. Here every file starts with:
- version - the version of the game (string)

### Tilemap

Then there is a long tilemap data, which is
- type - an array of the type of the block (currently is only 0)
- poses_x - an array of x positions
- poses_y - an array of y positions
The data is broken down to theese 3 parts to make the file a little bit shorter, but maybe I will make it different (until April)

### Objects
Here comes the interesting parts. The objects in the game

Here are all the parts:
- index - doesn't change anything, but must be unique

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

First value is a shape of the object (1 - box, 2 - circle, 3 - triangle). The second one is a texture, that is found in this table:
![Textures](https://raw.githubusercontent.com/R0fael/ClassBoom-Saving/refs/heads/main/resources/textures.png)

- sound - an array of two sounds(or effects), that are for collision and destruction(explosion or glass). Available sounds are: Bouncy, Explosion, Glass, Ice, Sand, Soft, Touch

- gluedObjects - an array of objects' id, that are glued to that object.

- components - an array of booleans, that enable some properties: Gluing(glues everything, what touches it), TNT(explodes on click), Booster(moves up, when clicked), Glass(Breaks, on collision)

- tntData - an array of values for tnt, that represents radius, force, time, randomness(randomied change of the explosion time)

- boosterData - force of the booster

- isSilent - means if doesn't has a collision sound
## Examples

Here I will show some examples of modified worlds.

### Developer World
A minimalistic world. Easier to modify

```json
{
    "version":"0.2.4",
    "tilemap":
    {"type":[0,0,0,0],"poses_x":[-2,-1,0,1],"poses_y":[-5,-5,-5,-5]},
    "objects":[
        {
            "index":0,
            "transform":[0,0,0,1,1],
            "rigidBodyData": [1,1,0],
            "constrains":0,
            "material":[0.4,0],
            "look":[1,33],
            "sounds":[6,4],
            "isSilent":false,
            "gluedObjects":[],
            "components":[false,false,false,false],
            "tntData":[0,0,0,0],"boosterData":[0]
        }    
    ]
}
```

### Elevator
Working elevator, that goes up

```json
{
    "version":"0.2.4",
    "tilemap":
    {"type":[0,0,0,0],"poses_x":[-2,-1,0,1],"poses_y":[-5,-5,-5,-5]},
    "objects":[
        {
            "index":0,
            "transform":[0,-4,0,5,1],
            "rigidBodyData": [1000,-1,5],
            "constrains":5,
            "material":[0.4,0.0],
            "look":[1,18],
            "sounds":[6,4],
            "isSilent":false,
            "gluedObjects":[],
            "components":[false,false,false,false],
            "tntData":[0,0,0,0],"boosterData":[0.0]
        }    
    ]
}
```
