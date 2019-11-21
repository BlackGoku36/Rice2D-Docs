# Debug

Version: `2019.11.17`

---

If you are using Git, then add [ZUI](https://github.com/armory3d/zui) submodule to your `Libraries`
and add following to your khafile.js
```
project.addLibrary('zui');
project.addDefine('rice_debug');
```

---

![](/../assets/d_1.png ':size=400')

![](/../assets/d_2.png ':size=200')
![](/../assets/d_3.png ':size=200')
![](/../assets/d_4.png ':size=200')

**Debug window**:
* **Outliner**: Show information about scene and it objects.
    * **Objects**: No. of object in scene.
    * **Assets**: No. of loaded assets for scene.
    * **Scene**: List of object in scene. `O` to select object, `X` to unselect object.
    * **Properties**: Properties of selected object (x, y, width, height, rotation, visibility).
* **FPS**: Show FPS
* **Console/last message**: Show the log
    * **Clear**: Clear the log
* **Prefs**: Preference of this debug window
    * **UI Scale**: Size of debug window.


**Debug of object**:
* X: x position of object
* Y: y position of object
* Width: width of object
* Height: height of object
* Rot: rotation of object in degrees

!> WIP
