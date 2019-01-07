Pcx - Point Cloud Importer/Renderer for Unity
=============================================

![GIF](https://i.imgur.com/zc6P96x.gif)
![GIF](https://i.imgur.com/lpWIiXu.gif)

**Pcx** is a custom importer and renderer that allows handling point cloud data
in Unity.

System Requirements
-------------------

- Unity 2017.3

Pcx uses the 32-bit vertex index format that is newly introduced in Unity
2017.3, so it's not compatible with the previous versions of Unity.

At the time this document is written, Unity 2017.3 is still in the beta testing
phase. Note that it possibly introduces some issues with the final released
version.

Supported Formats
-----------------

Currently Pcx only supports PLY binary little-endian format.

Installation
------------

Download and import one of the `.unitypackage` files from [Releases] page.

You can also use [Git support on Package Manager] to import the package. Add
the following line to the `dependencies` section in the package manifest file
(`Packages/manifest.json`). Note that this feature is only available from
Unity 2018.3. See [the forum thread][Git support on Package Manager] for
futher details.

```
"jp.keijiro.pcx": "https://github.com/keijiro/Pcx.git#upm"
```

[Releases]: https://github.com/keijiro/Pcx/releases
[Git support on Package Manager]:
    https://forum.unity.com/threads/git-support-on-package-manager.573673/

Container Types
---------------

![Inspector](https://i.imgur.com/Da0p6uV.png)

There are two types of container for point clouds.

### Mesh

Points are to be contained in a `Mesh` object. They can be rendered with the
standard `MeshRenderer` component. It's recommended to use the custom shaders
included in Pcx (`Point Cloud/Point` and `Point Cloud/Disk`).

### ComputeBuffer

Points are to be contained in a `PointCloudData` object, which uses
`ComputeBuffer` to store point data. It can be rendered with using the
`PointCloudRenderer` component.

There are no significant performance difference between these two container
types. The `ComputeBuffer` type is just convenient for animating points with
using compute shaders.

Rendering Methods
-----------------

There are two types of rendering methods in Pcx.

### Point (point primitives)

Points are rendered as point primitives when using the `Point Cloud/Point`
shader.

![Points](https://i.imgur.com/aY4QMtb.png)
![Points](https://i.imgur.com/jJAhLI2.png)

The size of points can be adjusted by the material properties.

![Inspector](https://i.imgur.com/gEMmxTH.png)

These size properties are only supported on some platforms; It may work with
OpenGLCore and Metal, but never work with D3D11/12.

This methods is also used when the point size is set to zero in
`PointCloudRenderer`.

### Disk (geometry shader)

Points are rendered as small disks when using the `Point Cloud/Disk` shader or
`PointCloudRenderer`.

![Disks](https://i.imgur.com/fcq5E3m.png)

This method requires geometry shader support.

Acknowledgements
----------------

The point cloud files used in the examples of Pcx are created by authors listed
below. These files are licensed under the Creative Commons Attribution license
([CC BY 4.0]). Please see the following original pages for further details.

- richmond-azaelias.ply - Azaleas, Isabella Plantation, Richmond Park.
  Created by [Thomas Flynn].
  https://sketchfab.com/models/188576acfe89480f90c38d9df9a4b19a

- anthidium-forcipatum.ply - Anthidium forcipatum ♀ (Point Cloud).
  Created by [Thomas Flynn].
  https://sketchfab.com/models/3493da15a8db4f34929fc38d9d0fcb2c

- Guanyin.ply - Guanyin (Avalokitesvara). Created by [Geoffrey Marchal].
  https://sketchfab.com/models/9db9a5dfb6744a5586dfcb96cb8a7dc5

[Thomas Flynn]: https://sketchfab.com/nebulousflynn
[Geoffrey Marchal]: https://sketchfab.com/geoffreymarchal
[CC BY 4.0]: https://creativecommons.org/licenses/by/4.0/

License
-------

[MIT](LICENSE.txt)
