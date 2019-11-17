# UI

Rice2D uses [ZUI](https://github.com/armory3d/zui) Canvas for UI.

If you are using Git, then add [ZUI](https://github.com/armory3d/zui) submodule to your `Libraries`
and add following to your khafile.js
```
project.addLibrary('zui');
project.addDefine('rice_ui');
```

Create new `canvas.json`(name can be whatever you want)

<!-- tabs:start -->
#### **canvas.json**

```json
{
    "name": "Canvas",
    "x": 0,
    "y": 0,
    "width": 400,
    "height": 400,
    "elements": [
        {
            "id": 0,
            "type": 0,
            "name": "myText",
            "x": 0,
            "y": 0,
            "width": 200,
            "height": 50,
            "text": "My Text",
            "color_text": -1513499
        }
    ]
}
```

* **name**: Name of canvas
* **x, y, width, height**: x, y, width and height properties of canvas.
* **elements**: List of elements(text, buttons, slider, etc)
    * **id**: Specific id of element.
    * **type**: Type of element, 0->Text, 1->Image, 2->Button, [etc](https://github.com/armory3d/zui/blob/9840d981f9916622710f883f4084488add43450f/Sources/zui/Canvas.hx#L315).
    * **name**: name of element.
    * **x/y/width/height**: x, y, width, height, properties of element.
    * **text**: Display text of element.
    * **color_text:** Colour of text in int.

You can check other options [here](https://github.com/armory3d/zui/blob/9840d981f9916622710f883f4084488add43450f/Sources/zui/Canvas.hx#L272)

#### **scene.json**
```json
{
    "name":"Scene",
    "canvasRef": "canvas",
    "assets":[...],
    "objects":[...]
}
```
* **canvasRef**: name of canvas file
<!-- tabs:end -->

!> WIP
