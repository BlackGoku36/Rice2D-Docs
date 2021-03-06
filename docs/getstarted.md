# Get Started

Version: `2020.5.0`

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
    ├── Sources
    │   ├─ scripts
    │   └── Main.hx
    └── khafile.js
```

To install `Rice2D`.
<!-- tabs:start -->

#### **Git(Recommended)**
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

1. Open `Main.hx` in `Source` folder.

<!-- tabs:start -->
#### **Main.hx**
```haxe
package;

import rice2d.App;

class Main {

    public static function main() {
        new App("Empty Rice2D", 720, 450, "");// 1
    }
}
```
* App(Title, width, height, clearColor, windowMode, scene)
    * **Title**: Title of the window.
    * **width**: Width of window.
    * **height**: Height of window.
    * **clearColor**: Background color (It is optional, it defaults to white).
    * **windowMode**: Mode of window, i.e, windowed or full-screen (It is optional, it defaults to windowed).
    * **scene**: json file of the scene.
<!-- tabs:end -->

Now, if you run it, you should get window with white screen.

---

## Scene

Scene is defined in json format.

1. Create `scene.json`.

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

This is basics structure of the scene. Now, let define our scene in `Main.hx`.

<!-- tabs:start -->
#### **Main.hx**
```haxe
package;

import rice2d.App;

class Main {

    public static function main() {
        new App("Empty Rice2D", 720, 450, "scene");// 1
    }
}
```
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
            "animated": true,
            "spriteRef": "blueguy"
        }
    ],
    "assets":[
        {
            "name": "blueguy",
            "type": 0
        }
    ]
}
```
* **objects.name**: Name of object.
* **objects.x**: X position of object.
* **objects.y**: Y position of object.
* **objects.width**: Width of object.
* **objects.height**: Height of object.
* **objects.animated**: If true, it will be subscale of the image(used for spritesheet animation), else normal scaled image.
* **objects.spriteRef**: Sprite reference of object in Assets.
* **assets**: List of assets.
* **assets.name**: Name of asset.
* **assets.type**: Type of asset (Image -> 0, Font -> 1, Sound -> 2, Blob -> 3).
<!-- tabs:end -->

Now playing, we should get:

![](/../assets/doc2.png ':size=600')

---

## Script

Script is code for an object functionality, multiple scripts can be attached to object (Similar to `Traits` in Iron/Armory).

Open `khafile.js` and add:
```
project.addParameter('scripts');
project.addParameter("--macro keep('scripts')");
```

And now create folder `scripts` inside `Sources` and inside this create `ScriptTest.hx`

<!-- tabs:start -->
#### **ScriptTest.hx**
```haxe
package scripts;

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
        notifyOnRender(function(g:kha.Canvas){
            var g2 = g.g2;
            g2.fillTriangle(350, 350, 250, 350, 350, 250);
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
            "animated": true,
            "spriteRef": "blueguy",
            "scripts": [
                {
                    "name": "OurScript",
                    "scriptRef": "ScriptTest"
                }
            ]
        }
    ],
    "assets":[
        {
            "name": "blueguy",
            "type": 0
        }
    ]
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
