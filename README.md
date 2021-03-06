# UniGLTF

[glTF](https://github.com/KhronosGroup/glTF) 2.0 importer and exporter for Unity 5.6 or later

Improved material importer(UniGLTF-1.21) ! 

Below is imported from [DamagedHelmet](https://github.com/KhronosGroup/glTF-Sample-Models/tree/master/2.0/DamagedHelmet). Using unity standard shader.

![standard shader](doc/pbr_to_standard.png)


![duck](doc/duck.png)
![animation](doc/animation.gif)

# License

* [MIT license](LICENSE)

# See also

* https://github.com/ousttrue/UniGLTF/wiki

# Sample Models

* https://github.com/KhronosGroup/glTF-Sample-Models

## Huge model required Unity2017.3 or later

* [Mesh.IndexFormat(from 2017.3)](https://docs.unity3d.com/ScriptReference/Mesh-indexFormat.html) is required

example. SciFiHelmet(70074vertices)

![SciFiHelmet](doc/SciFiHelmet.png)

# Download

* https://github.com/ousttrue/UniGLTF/releases

# Usage

## Import as prefab

* drop gltf folder or glb file into Assets folder

![duck_prefab](doc/duck_prefab.png)

or

* editor mode
* menu [UniGLTF] - [Import] 
* open gltf file(gltf, glb, zip) from out of Asset Folder

## Import in runTime

```cs
//
// UniGLTF-1.22
//
var path = UnityEditor.EditorUtility.OpenFilePanel("open gltf", "", "gltf,glb,zip");
if (string.IsNullOrEmpty(path))
{
    return;
}
Debug.LogFormat("open: {0}", path);

var context = new ImporterContext();
context.Load(path);
context.ShowMeshes();
context.EnableUpdateWhenOffscreen();
context.Root.name = Path.GetFileNameWithoutExtension(path);
```

## Import in runTime asynchronous

```cs
//
// UniGLTF-1.22
//
public static void LoadVrmAsync(string path, Byte[] bytes, Action<GameObject> onLoaded, Action<Exception> onError = null, bool show = true)
{
    var context = new ImporterContext();
    context.Parse(path, bytes);
    context.LoadAsync(onLoaded, onError, show);
}
```

## Export from scene

* select target root GameObject in scene(GameObect must be empty root, because target become gltf's ``/scene``. A scene includes nodes.
* menu [UniGLTF] - [Export]
* support only glb format

## Export in runTime

```cs
GameObject go; // export target
string path; // glb write path

var gltf = gltfExporter.Export(go);
var bytes = gltf.ToGlbBytes();
File.WriteAllBytes(path, bytes);
```

* support only glb format

