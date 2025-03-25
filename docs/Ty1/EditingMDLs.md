# Editing MDL Models

!!! warning "Animations"
    The plugin currently only has basic support for importing/exporting `rigging` (uses empties instead of bones as that was simpler to implement) and `weights`. The plugin doesn't support `editing animations` though

## Installation
To edit the models you're gonna need blender and the MDL2 blender plugin created by Kana.
!!! info "Supported Blender Versions"
    The Plugin Only Supports Blender Versions 3.0-4.3

To get started:

- Download the most recent version from the releases tab [https://github.com/ElusiveFluffy/MDL2-Blender-Plugin/releases](https://github.com/ElusiveFluffy/MDL2-Blender-Plugin/releases){:target="_blank"}
- Open blender and go to `Edit>Preferences>Add-ons`, and click on the install button at the top right
- Navigate to the zip file downloaded from the releases tab and select it
- Now just enable the plugin to have the MDL import and export options

## Importing Models

To import models just import then like any other model format in blender in the `file>import>MDL2` option.

When importing models if there is a `"DDS" folder` in the same folder as the MDL file with the required .dds textures, the importer will automatically load in the textures and set up the textures in the materials for you.

When importing the textures the plugin will automatically detect if it should be transparent. But sometimes the alpha check is incorrect and will result in models that should be opaque to be set as alpha blend.

## Setting the Texture
When exporting the exporter uses the `material names` for the texture names in the mdl.

Everything inside of the materials are **NOT** used when exporting, as the game mostly just supports diffuse textures and doesn't support the blender nodes, and to simplify exporting. 

If you're adding a texture to be used by the exported model all that is need is at least a empty material with its name the same as the texture's name (`excluding` the .dds part, which isn't needed in the name) or a name/alias of one in global.mad. 

!!! info "Exporting"
    The plugin will not export the dds textures with the model when exporting. Its expected that they're already in or modded into the game

## Sub Objects
Sub objects are created based on collections in blender, all meshes in a collection will be grouped into a sub object.

!!! info "Merged Sub Object Meshes"
    Since v1.3 the importer by default merges most of the meshes in each sub object together (it'll still keep the meshes in the right sub objects), for faster import times, and cleaner meshes in blender. This setting can be disabled in the import settings on the right side of the file selection window if needed.

Some examples of what sub objects are used for, or to keep in mind:

- Some actors in game will hide/show certain sub objects in certain situations, like Ty's bite head model, or the motion sub objects for rangs, etc.
- Each fragment mesh uses a sub object, more details about fragment meshes below.
- There is a limit of `32 bones` per sub object. If you need more bones for a model then you'll need to split the mesh up into multiple sub objects.
- Each mesh in a sub object seems to have a vertex count limit of `16383 vertices`. If you encounter crashing when trying to load your MDL in game one issue could be the vertex count being too high, so try splitting up some high poly meshes into multiple sub objects

## Adding Fragment Meshes
To add a fragment mesh all you need to do is have the fragment collection/sub object name start with `F_` (eg. `F_FragName`). This will automatically export that sub object as a fragment.

Keep in mind each individual fragment mesh will need to be in its own collection/sub object, if you want them to be separate, otherwise the fragment meshes in the same sub object will get grouped together into 1 fragment.

## Setting Collision Properties
Collisions are set through a custom collision panel, to easily select collision types (names taken from the comments in global.mad), with support for custom ones that you've added in the `global.mad` file.

!!! info "A couple things to note when setting a collision property"

    - If a collision property is set it will take priority over all of the texture names from the materials when exporting. Because of the way its set up with the collision panel each mesh can only have either texture names or a collision property.
    - If a mesh has a collision property it will typically be rendered `invisible`. This can be changed in `global.mad` but not fully recommended.

The collision panel is located in the `object data properties` tab
![CollisionPanel](../assets/Images/MDL2/CollisionPanel.PNG) ![CollisionPanel](../assets/Images/MDL2/CollisionTypes.PNG)

## Ref Points

`Ref points` can be for multiple different purposes depending on the model. Like with the flying platforms the ref points relate to where the particles should be emitted.

If a model contains `ref points` they will be imported as empties in a ref points collection.

!!! info "Exporting"
    Its recommended to have the same amount of ref points, with the same names, as the original model that you're editing/replacing.