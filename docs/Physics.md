# Physics

Rice2D uses Austin East 's [Echo library](https://austineast.dev/echo/) for physics.


If you are using Git, then add [Echo library](https://austineast.dev/echo/) and [hxmath](https://github.com/tbrosman/hxmath) submodule to your `Libraries`.

Physics can be simply enable by adding below to your game:

<!-- tabs:start -->
#### **scene.json**
```json
"name": "<Name of your scene>",
"physicsWorld": {
    "width": 720,
    "height": 450,
    "gravity_y":20,
    "iterations":3
},
"objects":[...],
"assets":[...]
```
* **physicsWorld**
    * **width**: Affects the bounds that collision checks.
    * **height**: Affects the bounds for collision checks.
    * **gravity_y**: Force of Gravity on y-axis of your physics world.
    * **iterations**: Sets the number of iterations each time the World steps.

You can check other options [here](https://github.com/AustinEast/echo/blob/bbaba615ce47b9981b5c6921c4671718edb06c66/echo/data/Options.hx#L89)

#### **khafile.js**
Add this to your khafile.
```
project.addLibrary('echo');
project.addLibrary('hxmath');
project.addDefine('rice_physics');
```

<!-- tabs:end -->

To add rigid body to your object, simply add:

<!-- tabs:start -->
#### **scene.json**
```json
{
    "name":"Scene",
    "canvasRef": "canvas",
    "physicsWorld":{
        "width": 1440,
        "height": 900,
        "gravity_y":2000,
        "iterations":3
    },
    "assets":[
        "playerAnim.png", "ground.png"
    ],
    "objects":[
        {
            "name": "player",
            "x":10,
            "y":10,
            "height": 256,
            "width": 256,
            "scripts": [...],
            "spriteRef": "playerAnim.png",
            "rigidBodyData": {
                "mass": 5,
                "shape": {
                    "type": 0
                }
            }
        }
    ]
}
```
* **rigidBodyData**
    * **mass**: Mass of the object, `0` -> Static rigidbody, `<Non-zero>` -> Dynamic rigidbody.
    * **shape**: Shape properties of the object.
        * **type**: Shape type of object. `0`->Rect, `1`->Circle, `2`->Polygon
        * **others**: `x`, `y`, `width`, `height`, `radius`(Circle), `array of vertices`(Polygon) can be defined. If they are defined than they will override x, y, etc of object for rigidbody, this is used for custom collision.

You can check other options [here](https://github.com/AustinEast/echo/blob/bbaba615ce47b9981b5c6921c4671718edb06c66/echo/data/Options.hx#L8)

<!-- tabs:end -->

!> WIP
