
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
