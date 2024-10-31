# General API

For more specific examples on how to use the functions you can look through the [<ins>Example Plugin</ins>](https://github.com/ElusiveFluffy/Example-Plugin){:target="_blank"}

## <h1> Functions: </h1>
### <h2> Initialize </h2>
---

Call this when the `TygerFramework Plugin Initialize` export function gets called, and `before` you call any other API functions.

<h3> Syntax </h3>

```C++
API::Initialize(param);
```

<h3> Parameters </h3>

`#!C++ param`

Type: `#!C++ TygerFrameworkPluginInitializeParam*`

The initialization parameter that gets passed to the plugin through the `TygerFramework Plugin Initialize` export function.

### <h2> IsInitialized </h2>
---
!!! tip "Only in v1.1.0 or newer ↓"

Call this to check if the API is initialized.  
Useful if you have a shutdown event and need to check if the API is initialized, to avoid a error occurring, incase the plugin unloaded early due to the wrong version of TygerFramework being installed

<h3> Syntax </h3>

```C++
API::IsInitialize();
```
<h3> Return Value </h3>

`#!C++ bool`

Returns `#!C++ true` if the API has been initialized.

### <h2> CurrentTyGame </h2>
---

Gets the currently running Ty Game

<h3> Syntax </h3>

```C++
API::CurrentTyGame();
```

<h3> Return Value </h3>

`#!C++ int`

Returns the current Ty game that is running.

- 0: Couldn't detect which game
- 1: Ty 1
- 2: Ty 2
- 3: Ty 3

### <h2> LogPluginMessage </h2>
---

Logs a message to the log `txt file` and to the `console`.

<h3> Syntax </h3>

```C++
API::LogPluginMessage(message, logLevel);
```

<h3> Parameters </h3>

`#!C++ message`

Type: `#!C++ std::string`

The message to be logged.

`#!C++ logLevel`

Type: `#!C++ LogLevel enum`

Default Value: `#!C++ Info`

The type of message your logging. `Doesn't need to be set for info`

Enum Values

- `#!C++ Info`
- `#!C++ Warning`
- `#!C++ Error`

### <h2> GetPluginDirectory </h2>
---
!!! tip "Only in v1.1.0 or newer ↓"

Gets the current plugin directory (is different between debug and release versions of TygerFramework. In debug versions its "Debug Plugins", in release versions its "Plugins")

<h3> Syntax </h3>

```C++
API::GetPluginDirectory();
```

<h3> Return Value </h3>

`#!C++ std::filesystem::path`

Returns the current path to the plugin directory.

### <h2> SetTyInputState </h2>
---
!!! tip "Only in v1.1.0 or newer ↓"

Sets the entire input flags state for the game from this plugin.

<h3> Syntax </h3>

```C++
API::SetTyInputState(flags);
```

<h3> Parameters </h3>

`#!C++ flags`

Type: [<ins>`#!C++ TyInputFlags enum`</ins>](GeneralAPI.md#tyinputsflags)

To see all the flags that can be set look at the [TyInputFlags section](GeneralAPI.md#tyinputsflags)

<h3> Return Value </h3>

`#!C++ bool`

Returns `#!C++ true` if the flags are successfully set.

<h3> Usage Examples </h3>

```C++
//Sets the entire state to the NoMouseClickInput flag
API::SetTyInputState(NoMouseClickInput);

//Setting multiple flags
API::SetTyInputState(NoMouseInput | NoKeyboardInput | TyShowCursor);
```

<h3> Remarks </h3>

The state flags from all plugins get combined together in TygerFramework to decide the state of the game. This is to avoid one plugin disabling a flag that another plugin needs enabled

### <h2> SetTyInputFlag </h2>
---
!!! tip "Only in v1.1.0 or newer ↓"

Function to more easily set or unset a flag(s) in some cases

<h3> Syntax </h3>

```C++
API::SetTyInputFlag(flag, enableFlag);
```

<h3> Parameters </h3>

`#!C++ flags`

Type: [<ins>`#!C++ TyInputFlags enum`</ins>](GeneralAPI.md#tyinputsflags)

To see all the flags that can be set look at the [TyInputFlags section](GeneralAPI.md#tyinputsflags)

`#!C++ enableFlag`

Type: `#!C++ bool`

`#!C++ true` to enable/set the flag,  
`#!C++ false` to disable/unset the flag

<h3> Return Value </h3>

`#!C++ bool`

Returns true if successfully set the flags.

<h3> Usage Examples </h3>

```C++
//Just setting 1 flag to be enabled, 
//without changing the state of any of the other flags that may be set
API::SetTyInputFlag(NoMouseClickInput, true);

//Unsetting/setting multiple flags
API::SetTyInputFlag(NoMouseInput | NoKeyboardInput | TyShowCursor, false);
```

<h3> Remarks </h3>

The state flags from all plugins get combined together in TygerFramework to decide the state of the game. This is to avoid one plugin disabling a flag that another plugin needs enabled

### <h2> GetTyInputState </h2>
---
!!! tip "Only in v1.1.0 or newer ↓"

Get the current input state of the game set by your plugin

<h3> Syntax </h3>

```C++
API::GetTyInputState();
```

<h3> Return Value </h3>

[<ins>`#!C++ TyInputFlags enum`</ins>](GeneralAPI.md#tyinputsflags)

Returns the currently set [Ty Input Flags](GeneralAPI.md#tyinputsflags).

<h3> Usage Examples </h3>

```C++
//Get the current flags
TyInputFlags flags = API::GetTyInputState();

//Which can then be used for something like toggling a flag with a bitwise XOR
//Each time this is run it'll alternate between setting and unsetting the flag
API::SetTyInputFlag(flags ^ NoMouseInput);

//Can also be used to check if a specific flag(s) is set with the bitwise AND
if (flags & NoKeyboardInput){

}
```

<h3> Remarks </h3>

Keep in mind that this doesn't get the state of other plugins, so the game could be blocked by a different plugin, which this won't say.

The state flags from all plugins get combined together in TygerFramework to decide the state of the game. This is to avoid one plugin disabling a flag that another plugin needs enabled


## <h1> Variables: </h1>

### <h2> TyHModule </h2>
---

Can be used to get the base address of the game by casting it to a `#!C++ DWORD`.

<h3> Syntax </h3>

=== "v1.0.1"
    ```C++
    API::Get()->param()->TyHModule;
    ```

=== "v1.0.0"
    ```C++
    API::Get()->param()->tygerFrameworkModule;
    ```

Type: `#!C++ HMODULE`


### <h2> initErrorMessage </h2>
---

Only to be used for when you would `#!C++ return false` in the `TygerFramework Plugin Initialize` export function. More info on the [<ins>Error Message</ins>](../index.md#error-message) section on the Getting Started page

Gives more info for what went `wrong` during initialization of your plugin.

<h3> Syntax </h3>

```C++
API::Get()->param()->initErrorMessage = "Write what went wrong here";
```
Type: `#!C++ std::string`

### <h2> TyInputsFlags </h2>
---
!!! tip "Only in v1.1.0 or newer ↓"

Used in the [SetTyInputState](GeneralAPI.md#settyinputstate), [SetTyInputFlag](GeneralAPI.md#settyinputflag), and [GetTyInputState](GeneralAPI.md#settyinputstate) functions

Type: `#!C++ enum`

Enum Values

- `#!C++ None //No flags set`
- `#!C++ NoMouseClickInput //Only mouse clicks disabled`
- `#!C++ NoMouseCameraInput //Only mouse camera movement disabled`
- `#!C++ NoKeyboardInput //Disables all keyboard input`
- `#!C++ TyShowCursor //Shows and unlocks the mouse cursor`
- `#!C++ NoMouseInput //Disables both mouse clicks and mouse camera movement`
