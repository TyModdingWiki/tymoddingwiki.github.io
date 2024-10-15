# Getting Started

!!! info "Note"
    This guide will go over how to make a plugin using a `C++ visual studio project`, but you could also use cmake, but you'll need to do things a bit differently, which won't be covered here.
    
!!! tip "Version"
    Everything in this wiki is based on `v1.0.0` of TygerFramework, unless specified otherwise

## Adding the API

First you'll need to set your C++ version to `C++17` as thats the version the API needs. To set it just right click on the `project` then `Properties>General>C++ Language Standard`. Click on it and a arrow to the right will appear and clicking on that will have a dropdown of all the available versions. Just set it to `atleast C++17 or newer`.

To include the API for the plugin just download the `API for Developing Plugins zip` from the releases tab: [<ins>https://github.com/ElusiveFluffy/TygerFramework/releases<ins>](https://github.com/ElusiveFluffy/TygerFramework/releases){:target="_blank"}.

Then just copy the `TygerFrameworkAPI.h` and `TygerFrameworkAPI.hpp` files into the project folder, then in visual studio add them as a existing item. If you `don't copy` them to the project folder it'll just reference the original location for the file. Which can cause `issues or make it more difficult when trying to include it`.

Now just add `#!C++ #include "TygerFrameworkAPI.hpp"` to any classes that you want to use the API with.
!!! warning "Use the .hpp not .h"
    Make sure to `#!C++ #include` the `.hpp` file and `not the .h` file

## Initializing the API

Now that the API is included you need to `initialize` the API. A nice place to do this is in `dllmain.cpp`, so add the `API hpp` file to dllmain.

To initialize the API create a export function either like
```C++
EXTERN_C bool TygerFrameworkPluginInitialize(TygerFrameworkPluginInitializeParam* param) {
    //Make sure to call this first before any API Functions
    API::Initialize(param);
}
```
or
```C++
extern "C" __declspec(dllexport) bool TygerFrameworkPluginInitialize(TygerFrameworkPluginInitializeParam* param) {
    //Make sure to call this first before any API Functions
    API::Initialize(param);
}
```
From this function you need to return a bool. `#!C++ return true` if your plugin `successfully` initialized, or `#!C++ false` if your plugin `failed` to initialize some code you needed. Returning false will make TygerFramework `unload` your plugin

### Error Message
If you `#!C++ return false`, you can also set a `error message` to give more info about what went wrong. It will also show the error in the plugin collapsed header in the TygerFramework window.

No need to also log the error, as TygerFramework will do that for you with the error message you provide.

To set the error message you just need to set the `#!C++ initErrorMessage` variable in the `#!C++ param` like this:
```C++
if (ErrorCondition) {
    param->initErrorMessage = "Write what went wrong here";
    return false;
}
```

## Plugin Minimum Version Requirement
Its recommend to add the minimum version requirement function so your plugin `won't be loaded with a older version` of TygerFramework, and crash the game if it tries using API functions that aren't in the older version.

The API files `include` definitions for which version it is intended for, so you can easily specify which version the plugin needs.

To add the function you can add it either like this
```C++
EXTERN_C void TygerFrameworkPluginRequiredVersion(TygerFrameworkPluginVersion* version) {
    //Use the version number defined in the API
    version->Major = TygerFrameworkPluginVersion_Major;
    version->Minor = TygerFrameworkPluginVersion_Minor;
    version->Patch = TygerFrameworkPluginVersion_Patch;

    //Optional if you only want the plugin to run for a specific game 
    //(List all the game numbers the plugin is compatible with (1 = Ty 1, 2 = Ty 2, 3 = Ty 3). 
    //If you don't include this line it'll support any game)
    version->CompatibleGames = {1};
}
```
or
```C++
extern "C" __declspec(dllexport) void TygerFrameworkPluginRequiredVersion(TygerFrameworkPluginVersion* version) {
    //Specifiy the version number defined in the API
    version->Major = TygerFrameworkPluginVersion_Major;
    version->Minor = TygerFrameworkPluginVersion_Minor;
    version->Patch = TygerFrameworkPluginVersion_Patch;

    //Optional if you only want the plugin to run for a specific game 
    //(List all the game numbers the plugin is compatible with (1 = Ty 1, 2 = Ty 2, 3 = Ty 3). 
    //If you don't include this line it'll support any game)
    version->CompatibleGames = {1};
}
```

The compatible games line is `only required` if you want your plugin to only load for a certain game.

!!! abstract "Load Order"
    The minimum version function gets checked `before` the plugin gets initialized with the `TygerFrameworkPluginInitialize` function

## Adding the Export Functions

If you're using a C++ project file make sure to also add a `Source.def` file. To create one with the add new file menu go to the `code section` then `Module-Definition File`. To make sure it auto linked right click on the `project` then `Properties>Linker>Input` and the `Source.def` file should be in the module definition file section, if not just add it in there.

Next you need to specify the export functions in your `Source.def` file, open it and add your plugin name next to `LIBRARY` and add the `EXPORTS` you're using
```C++
LIBRARY "Example Plugin"

EXPORTS
TygerFrameworkPluginInitialize
TygerFrameworkPluginRequiredVersion
```
Of course replacing `"Example Plugin"` with your own project name, the quotation marks are only needed if your project name has a space in it.

!!! info "Building"
    Now you should be able to build the project and TygerFramework should be able to initialize your plugin with the API, and check the minimum required version

## Post Build Command

I `highly recommend` adding a post build command to auto copy the built dll to the plugin folder, as it makes it `alot more convenient` to test the plugin without having to copy the dll to the plugin folder every time you recompile it.

To add one just right click on the project file then `properties>Build Events>Post-Build Event`, in the command line section add this command:
```batch
copy "$(OutDir)$(ProjectName).dll" "C:\Program Files (x86)\Steam\steamapps\common\TY the Tasmanian Tiger\Plugins\$(ProjectName).dll"
```
Of course `changing the path to the game` to where you have Ty 1, 2, or 3 installed.

## Debugging Your Plugin

To `debug` your plugin with `breakpoints` you just need to set `2` things in the properties of the project. Just right click on the `project` then `Properties>Debugging`

Inside the Debugging section you need to set the `Command` to the Ty exe.  
If you click in the text box a arrow will appear on the right side, clicking on that you can then `choose browse` to be able to just browse to the exe.

You next need to set the `Working Directory` to the `folder` the Ty exe is in, otherwise the game will look for the RKVs in the `wrong folder` and just `crash` because they aren't there.  
You can also do the same `browse` thing as you did with the `Command section`.

Now that you have the Debugging settings all set up you can just press the `play button` (Will say `Local Windows Debugger`) in visual studio and it will launch the game and `trigger any breakpoints` you have set in the code for the plugin.

!!! note "Launch Options"
    You can also add any launch options you want, (like -tydev), in the `Debugging` settings in the `Command Arguments` section

## DllMain

Optionally, you can use `DllMain for startup`, with `DLL_PROCESS_ATTACH`, if your plugin absolutely needs to load `immediately`, or you don't want the TygerFramework API.

DllMain will get loaded earlier than the `TygerFramework Plugin Initialize` export function, and will `hold up the game` unless you make another thread.

## Example Plugin
If you prefer going through a already made plugin, or need to see how it works in a actual project, I've created a example plugin of how you would go about using the API. [<ins>https://github.com/ElusiveFluffy/Example-Plugin</ins>](https://github.com/ElusiveFluffy/Example-Plugin){:target="_blank"}.

A version for each TygerFramework release can be found in the releases tab, which includes the source code and a built DLL of the example plugin.