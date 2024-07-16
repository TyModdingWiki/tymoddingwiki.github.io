# Getting Started

This page will walk you through the basics you'll need to know to get started with modding Ty 1.

## Extracting the rkvs

To get started with extracting the rkvs to edit the game files you'll need Koushi's tool called rkvMT (or Chippy's [rkv extractor](https://github.com/1superchip/Rkv-Extractor){:target="_blank"}, but for this guide we'll use rkvMT)  

- Download rkvMT here [https://github.com/tanoshiikoushi/rkvMT/releases](https://github.com/tanoshiikoushi/rkvMT/releases){:target="_blank"}
- After downloading launch the exe, it'll open up a console window, but don't worry its not too complex to use
- First load the rkv you want to extract, the main rkv you'll probably want to extract is Data_PC.rkv, which contains most of the game's files. For this example I'll load the rkv into the out slot.  
You can more easily enter the folder by copying the folder path in the path text box at the top of file explorer
```
load "C:/path/to/Data_PC.rkv" out
```
- Next extract the whole rkv that was loaded into the out slot to any folder you want
```
extract out * "C:/path/to/extract/to" true
```
- Now just wait for it to extract all the files and you're done

## Editing the files

Now that you have the files extracted you may be wondering how to edit them, below are some of the ways you can edit some common files. All of the files mentioned below are all stored in `Data_PC.rkv`.

If the kind of file you're looking for isn't listed below, either try searching the wiki or ask in the modding discord.

### Textures

Editing the texture files is pretty simple, they're all stored in the `DDS folder` and can easily be opened by basically any image editing software (like gimp).  
To export the dds files there is certain format settings to make sure that you use depending on the texture file. Its also recommended to enable generating mipmaps too

If the texture has `no transparency` export the dds with the `DXT1` format

If the texture `has transparency` export it with the `DXT5` format

If you don't use those setting the colour channels will be flipped, or the transparency won't work.

### Level object placement

Level object files are pretty easy to edit as they're just plain text, you can just open the `.lv2` files in any text editor. Unfortunately right now there is no level editor to easily edit the object placement in levels, but the is a program called Ty pos which displays Ty's in game coordinates, which helps to figure out where to place objects.  
There is 3 different versions:

- [Pixel's version (In the Ty speedrunning discord)](https://discord.com/channels/161894912080478208/706965938830049401/910153993265758240){:target="_blank"}
- Buzchy's version which includes rotation [https://github.com/Senashu/TyPos-Rotation](https://github.com/Senashu/TyPos-Rotation){:target="_blank"}
- [Matt's version (In the modding discord)](https://discord.com/channels/1029229401314967562/1029419492641615903/1077002267271626762){:target="_blank"} which includes logging but no rotation.

### Object properties

A lot of the object properties are stored within the `global.model` file, which is also plain text, so just open it with any text editor. The file contains alot of different properties like stuff about enemies, the boomerangs, render distances, etc.  
Not everything is in that file though and some are hard coded in the exe.

There is another similar file called `global.mad`, which is also, you guessed it, plain text. This file contains properties that materials and collision materials have, like if it has grass on it, what sound to make, what particle effect to make, is it slippery, etc.  
All the property IDs are listed at the top of the file, and multiple properties can be combined by just adding the numbers together.

### Models

Models are stored in the `.mdl` files and can be imported and exported in blender using Kana's Ty 1 mdl plugin [https://github.com/ElusiveFluffy/MDL2-Blender-Plugin](https://github.com/ElusiveFluffy/MDL2-Blender-Plugin){:target="_blank"}.  
All the documentation on how to use the plugin is in the readme on the github page.

## Loading modified game files

There is 2 different ways to load the files you've modified into the game, either using the PC_External folder or creating a Patch_PC.rkv.  
Using PC external is easier to quickly test different changes to the files, but it's more limited. Some files will only load with the debug OpenAL dll (like mdl files), and some won't load at all in there (like ogv files).  
Only downsides is the debug OpenAL breaks bosses by not allowing you to enter the boss fights for the first time, even if you have enough thunder eggs. It also breaks the level select, and can sometimes glitch some textures.

### PC_External

First thing to do for the PC_External method is to create a folder in the game folder and make sure to name the folder exactly like `"PC_External"`.  
Now just copy any modified files into that folder. **They do not need to be in the same sub folders they were extracted to, just put them in the root of PC_External**  
To use the debug openAL, which can download it from here [Debug OpenAL32.dll](../assets/OpenAL/DebugOpenAL32.dll){:download="OpenAL32.dll"}, and just put it in the folder for the game replacing the one already there (recommend making a copy of the original one, just to easily be able to swap between them).

If you didn't make a copy of the original OpenAL you can either verify the file integrity in steam or download it here [Retail OpenAL32.dll](../assets/OpenAL/RetailOpenAL32.dll){:download="OpenAL32.dll"}.

### Creating a Patch_PC rkv

Creating a Patch_PC rkv is more recommended for a completed mod, just so you don't have to keep regenerating the rkv every time you make changes to any files.

- To create one make a folder with all the files you want to pack into the rkv (Make sure all the files aren't in any sub folders)
- Make a folder called "Dummy" next to it with nothing in it
- Launch rvkMT
- Inside rvkMT load the folder into the in slot
```
load_dir "C:/path/to/modified/files" ../Dummy in
```
- Next generate the rkv
```
generate in
```
- Then finally save the rkv to where you have Ty installed with `Patch_PC.rkv` after the path
```
save in "C:/path/to/ty/folder/Patch_PC.rkv"
```

Now you can launch the game with no files in PC_External and it should load all your modified files from the Patch_PC.rkv with the retail OpenAL


For more info about rvtMT you can look at the readme on the git repo for it [https://github.com/tanoshiikoushi/rkvMT](https://github.com/tanoshiikoushi/rkvMT){:target="_blank"}