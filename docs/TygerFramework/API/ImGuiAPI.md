# API for ImGui

For more specific examples on how to use the functions you can look through the [<ins>Example Plugin</ins>](https://github.com/ElusiveFluffy/Example-Plugin){:target="_blank"}

## GetTyWindowHandle
---

<h3> Syntax </h3>

```C++
API::GetTyWindowHandle();
```

<h3> Return Value </h3>

`#!C++ HWND`

Returns the current Ty window handle, or `#!C++ nullptr` if TygerFramework had a issue getting the handle (most of the time it should be fine).

## DrawingGUI
---

<h3> Syntax </h3>

```C++
API::DrawingGUI();
```

<h3> Return Value </h3>

`#!C++ bool`

Returns `#!C++ true` if the TygerFramework menu is currently open.

## SetImGuiFont
---

Sets the ImGui font to be the same as TygerFramework's main window

<h3> Syntax </h3>

```C++
API::SetImGuiFont(ImGui::GetIO().Fonts);
```
<h3> Parameters </h3>

`#!C++ imguiFont`

Type: `#!C++ void*`

Your ImGui Font pointer.

## SetTygerFrameworkImGuiElements
---

`Doesn't Need ImGui Installed`

Sets the elements from the plugin that will be drawn below the plugin section in the TygerFramework ImGui window.

`Overwrites` the old value if its called again

<h3> Syntax </h3>

```C++
API::SetTygerFrameworkImGuiElements(elements)
```

<h3> Parameters </h3>

`#!C++ elements`

Type: `#!C++ std::vector<TygerFrameworkImGuiParam>`

All the elements that will be rendered in the TygerFramework ImGui window.

`#!C++ TygerFrameworkImGuiParam`

Type: `#!C++ struct`

- First element is a `#!C++ enum` for which element to draw
- Second element is a `#!C++ std::string` for if the element needs text

Enum values:

- `#!C++ CollapsingHeader //Needs text for header name`
- `#!C++ Text //Needs text`
- `#!C++ TextWrapped //Needs text`
- `#!C++ SameLine //No text`
- `#!C++ NewLine //No text`
- `#!C++ Spacing //No text`
- `#!C++ SetTooltip //Needs text for tooltip (Adds a tooltip to the previous element)`
- `#!C++ TreePush //Needs text for tree internal name`
- `#!C++ TreePop //No text (Make sure to call when done after using TreePush)`

<h3> Usage Example </h3>

```C++
void GUI::SetFrameworkImGuiElements()
{
    namespace fs = std::filesystem;
    //Setting the values for GUI to render on the TygerFramework window
    //Only a few basic elements available as its mainly intended to 
    //just be for adding basic stuff to the TygerFramework window 
    std::vector<TygerFrameworkImGuiParam> TygerFrameworkImguiElements = { 
        {CollapsingHeader, "Example Plugin"},
        {Text, "Files in Ty Directory Example"},
        {SameLine},
        {Text, "(?)"},
        {SetTooltip, "Just an Example of Iterating and Adding Elements"},
        {TreePush, "Example Plugin"} };
    //Looping through elements and adding them 
    //as a example of iterating and adding elements
    for (auto&& entry : fs::directory_iterator{ fs::current_path() }) {
        auto&& path = entry.path();
        TygerFrameworkImguiElements.push_back({ Text, path.filename().string()});
    }

    TygerFrameworkImguiElements.push_back({ TreePop });

    API::SetTygerFrameworkImGuiElements(TygerFrameworkImguiElements);

    API::LogPluginMessage("Set TygerFramework ImGui Functions");
}
```