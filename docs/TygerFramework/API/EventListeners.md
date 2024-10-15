# Event Listeners

For more specific examples on how to use the functions you can look through the [<ins>Example Plugin</ins>](https://github.com/ElusiveFluffy/Example-Plugin){:target="_blank"}

## AddDrawPluginUI
---

<h3> Syntax </h3>

```C++
API::AddDrawPluginUI(func);
```

Input function just needs to be void:
```C++
void DrawUI()
```

<h3> Parameters </h3>

`#!C++ func`

The function you want to be ran `every frame` that the TygerFramework menu is `open`.

<h3> Return Value </h3>

`#!C++ bool`

If the input function is successfully subscribed to the `draw plugin UI event` it'll return `#!C++ true`.

## AddPluginImGuiWantCaptureMouse
---

Required for `fixing the resize cursor` on plugin windows, and to `stop` the game from registering inputs while the window is focused

<h3> Syntax </h3>
=== "v1.0.1"

    ```C++
    //Make sure to cast this, otherwise TygerFramework won't get the return value
    API::AddPluginImGuiWantCaptureMouse((ImGuiWantCaptureMouseFunc)func);
    ```

=== "v1.0.0"

    ```C++
    //Make sure to cast this, otherwise TygerFramework won't get the return value
    API::AddPluginImGuiHasFocus((ImGuiHasFocusFunc)func);
    ```

All your event function needs to contain:
```C++
//To block clicks from the game when the window is focused
bool GUI::ImGuiWantCaptureMouse() {
    //WantCaptureMouse works better than window focus
    return ImGui::GetIO().WantCaptureMouse;
}
```
`#!C++ return:`  
Just return your plugin's ImGui WantCaptureMouse state.

<h3> Parameters </h3>

`#!C++ func`

The function you want to be used to check if your plugin's ImGui context has any windows that want mouse capture.

<h3> Return Value </h3>

`#!C++ bool`

If the input function is successfully subscribed to the `ImGui want capture mouse event` it'll return `#!C++ true`.

## AddPluginWndProc
---

Required for `interacting` with your ImGui window.  
Also used to block any WndProc events from the game by returning `#!C++ true`.

<h3> Syntax </h3>

```C++
//Make sure to cast this, otherwise TygerFramework won't get the return value
API::AddPluginWndProc((WndProcFunc)func);
```

Minimal amount that you may typically need for your plugin:
```C++
//WndProc to be able to interact with imgui or block any WndProc from interacting with the Ty window
extern LRESULT ImGui_ImplWin32_WndProcHandler(HWND hWnd, UINT msg, WPARAM wParam, LPARAM lParam);
bool WndProc(HWND hWnd, UINT msg, WPARAM wParam, LPARAM lParam) {
    if (API::DrawingGUI())
        if (ImGui_ImplWin32_WndProcHandler(hWnd, msg, wParam, lParam))
            return true;
    return false;
}
```

<h3> Parameters </h3>

`#!C++ func`

The function you want any WndProc events to be sent to.

<h3> Return Value </h3>

`#!C++ bool`

If the input function is successfully subscribed to the `WndProc event` it'll return `#!C++ true`.

## AddPluginWndProc
---

Tick event that runs every frame `before` the game runs its own logic.

<h3> Syntax </h3>

```C++
API::AddTickBeforeGame(func);
```

Input function just needs to be void and have a float input:
```C++
void TickBeforeGame(float deltaSeconds)
```

<h3> Parameters </h3>

`#!C++ func`

The function you want to be ran `every frame before` the game's logic.

`#!C++ deltaSeconds`

The amount of seconds the last frame took to render.

<h3> Return Value </h3>

`#!C++ bool`

If the input function is successfully subscribed to the `tick before game event` it'll return `#!C++ true`.