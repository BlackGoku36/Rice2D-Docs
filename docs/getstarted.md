# Get Started

Version: `2019.11.17`

---

Table of contents:
* [Init project](#init-project)
* [Window](#window)
* [Scene](#scene)
* [Script](#script)

---

## Init project
Init kha project, if you haxe VS-Code kha extension, press `F1` and enter `Init Kha Project`, else clone [Kha empty project](https://github.com/Kha-Samples/Empty).

Let create some new folder for later use: `Libraries`, `Assets`.

You should have something like this:
```
Empty
    ├── Assets
    ├── Libraries
    ├── README.md
    ├── Kha
    ├── Sources
    │   └── Main.hx
    └── khafile.js
```

To install `Rice2D`.
<!-- tabs:start -->

#### **Git**
Navigate to `Libraries` folder and add `Rice2D` submodule.
```
git submodule add https://github.com/BlackGoku36/Rice2D
```

#### **Haxelib**
Install `Rice2D` through `haxelib`
```
haxelib install Rice2D
```
<!-- tabs:end -->

and finally add `Rice2D` library to `khafile.js`:
```
project.addLibrary('rice2d');
```

---

## Window
Window and it properties is defined in `window.json`, engine will automatically pick up `window.json` in `Assets` folder.

Create `window.json` inside `Assets`, this is used to define window properties.

<!-- tabs:start -->
#### **window.json**
```json
{
    "name":"Empty Rice2D",
    "width": 720,
    "height": 450,
    "windowMode": 0
}
```
* **name**: Title for window
* **width**: Width of window
* **height**: Height of window
* **windowMode**: Mode of window, 0 is windowed screen and 1 is fullscreen.
<!-- tabs:end -->

Now open `Main.hx`.
<!-- tabs:start -->
#### **Main.hx**
```haxe
package;

import rice2d.App;

class Main {

    public static function main() {
        new App("");// 1
    }
}
```
1. Create new App with no scene
<!-- tabs:end -->

Now, if you run it, you should get black window:

![](/../assets/doc1.png ':size=600')

---

## Scene

Scene is defined in json format ofc! Let create `scene.json`, unlike window, scene's json can have whatever name you want.

<!-- tabs:start -->
#### **scene.json**
```json
{
    "name": "MyScene",
    "objects":[],
    "assets":[]
}
```
* **name**: Name of scene.
* **objects**: List of objects.
* **assets**: List of assets.
<!-- tabs:end -->

This is basics structure of the scene. Now, let define our scene in `Main.hx`, it easy peasy!

<!-- tabs:start -->
#### **Main.hx**
```haxe
package;

import rice2d.App;

class Main {

    public static function main() {
        new App("scene");// 1
    }
}
```
1. We define scene in parameter of `new App()`.
<!-- tabs:end -->

And this is how you define a scene, now let add [blue guy](https://github.com/BlackGoku36/Rice2D-Empty/blob/master/Assets/blueguy.png) from Lewis Lepton tutorial to our scene.

Add blue guy to `Assets` folder and open `scene.json`

<!-- tabs:start -->
#### **scene.json**
```json
{
    "name": "MyScene",
    "objects":[
        {
            "name": "object",
            "x": 150,
            "y": 150,
            "width": 256,
            "height": 256,
            "spriteRef": "blueguy.png",
            "scripts": []
        }
    ],
    "assets":["blueguy.png"]
}
```
* **objects.name**: Name of object.
* **objects.x**: X position of object.
* **objects.y**: Y position of object.
* **objects.width**: Width of object.
* **objects.height**: Height of object.
* **objects.spriteRef**: Sprite reference of object in Assets.
* **assets**: Asset reference.
<!-- tabs:end -->

Now playing, we should get:

![](/../assets/doc2.png ':size=600')

---

## Script

Script is code for an object functionality, multiple scripts can be attached to object (Similar to `Traits` in Iron/Armory).

Open `khafile.js` and add:
```
project.addParameter('rice');
project.addParameter("--macro keep('rice')");
```

And now create folder `rice` inside `Sources` and inside this create `ScriptTest.hx`

<!-- tabs:start -->
#### **ScriptTest.hx**
```haxe
package rice;

class ScriptTest extends rice2d.Script{

    public function new() {
        super();
        // 1
        notifyOnInit(function(){
            trace("Init!");
        });
        // 2
        notifyOnUpdate(function(){
            trace("Update!");
        });
        // 3
        notifyOnRender(function(g:kha.graphics2.Graphics){
            g.fillTriangle(350, 350, 250, 350, 350, 250);
        });

    }

}
```
1. **notifyOnInit**: Execute function when the script is initiated. Here, we will output `Init!`.
1. **notifyOnUpdate**: Execute function every frames. Here, we will output `Update!`.
1. **notifyOnRender**: Execute function during rendering. Here, we will draw a filled triangle from 3 vertices position.

<!-- tabs:end -->

Now to attach `ScriptTest.hx` to our object:

<!-- tabs:start -->
#### **scene.json**
```json
{
    "name": "MyScene",
    "objects":[
        {
            "name": "object",
            "x": 150,
            "y": 150,
            "width": 256,
            "height": 256,
            "spriteRef": "blueguy.png",
            "scripts": [
                {
                    "name": "OurScript",
                    "scriptRef": "ScriptTest"
                }
            ]
        }
    ],
    "assets":["blueguy.png"]
}
```
* **objects.scripts.name**: Name of script.
* **objects.scripts.scriptRef**: Script class reference.
<!-- tabs:end -->

Now if you play, you should get something like:

![](/../assets/doc3.png ':size=600')

Output:

```
rice/ScriptTest.hx:9: Init!
rice/ScriptTest.hx:13: Update!
rice/ScriptTest.hx:13: Update!
...
rice/ScriptTest.hx:13: Update!
```

---

That is! We completed basics!

If you had any problem, check out [Rice2D-Empty](https://github.com/BlackGoku36/Rice2D-Empty)
