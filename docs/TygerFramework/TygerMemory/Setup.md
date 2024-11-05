# Quickstart

!!! info "Note"
    TygerMemory is a dependency used by TygerFramework and as such should be used with TygerFramework. While it can be used separately, this may require more extensive linker settings and setup.

## What is Tyger Memory?

Tyger Memory is an extension to the Tyger Framework API which exposes high level functions and structures for manipulating the running memory of the games to developers, handling the low level calls in the background. 

!!! warning "Compatibility"
    So far, only Ty the Tasmanian Tiger 1 is supported by TygerMemory. The functions provided by the API will produce undefined behaivour on the other games. TygerMemory2 and TygerMemory3 may be created in the future. 

If you're only looking to use plugins and someone has sent you to this page, all you need to do is download the correct (usually the latest) version of the TygerMemory.dll and add it to your 'Plugins/Dependencies' directory. The other files are not needed.

If you're here as a developer wanting to make a plugin, you're best starting with [setting up TygerFramework](../index.md). Once you have your first plugin building, it's time to implement TygerMemory.

### Adding TygerMemory

The first thing you'll need to do is head over to the [TygerMemory1 Github releases page](https://github.com/xMcacutt/TygerMemory1/releases) and download the TygerMemoryAPI.zip. This file contains all of the required header files in an include folder as well as the .lib build of the API. 

!!! info "Note"
    The following section assumes you are using a Visual Studio C++ dll project **without** CMake. This isn't necessary but the steps will be different for CMake builds.

Add the include directory to your project include directories by right-clicking the project in the solution explorer and going to Properties -> Configuration Properties -> Include Directories

Set the linker to link TygerMemory.lib by right-clicking your project and choosing Add -> Existing Item and selecting TygerMemory.lib. This will add the library as source. Along with the header files being included, this is sufficient for usage.

If you're developing several plugins, you may either

- Keep a single instance of the API files somewhere and have all projects reference it. This way, you only need to update the single instance and then your projects' references to the API files when a new update is released.

- Copy the API files you your project each time so that each project is built with a specific version of the API. If, for a given project, you don't expect to need new features as they are released, this is the better option.

Make sure the header files and the library you are using are from the same build of the API. Mismatched versions often lead to linker or invalid dll entry point errors.

---

## Starting Coding

Once you're set up, you need to include the "core.h" header file in your plugin's entry point. After initializing or in the initialization method for TygerFramework, you can call

```cpp
Core::initialize((HMODULE)API::Get()->param()->TyHModule);
```

This initializes the API to allow it to read from the game's memory by providing it the .exe module handle.

The [Ty Collectible Tracker Plugin](https://github.com/xMcacutt/Ty-Collectible-Tracker-Plugin) can be used as an example in case you get stuck.

---

## Next Steps

Now you're set up, you can use any of the many classes to interact with Ty's memory. The docs here provide descriptions of each of the functions and their limitations but these are also provided via xml tags on the functions themselves.

A good starting place for understanding how to work with TygerMemory is the [hero class](./Classes/Hero.md)