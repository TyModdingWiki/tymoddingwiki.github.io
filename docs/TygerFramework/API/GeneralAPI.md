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

Type: `#!C++ enum`

Default Value: `#!C++ Info`

The type of message your logging. `Doesn't need to be set for info`

Enum Values

- `#!C++ Info`
- `#!C++ Warning`
- `#!C++ Error`

## <h1> Variables: </h1>

### <h2> TyHModule </h2>
---

<h3> Syntax </h3>

Can be used to get the base address of the game by casting it to a `#!C++ DWORD`.

=== "v1.0.1"
    ```C++
    API::Get()->param()->TyHModule;
    ```

=== "v1.0.0"
    ```C++
    API::Get()->param()->tygerFrameworkModule;
    ```

    
### <h2> initErrorMessage </h2>
---

<h3> Syntax </h3>

Only to be used for when you would `#!C++ return false` in the `TygerFramework Plugin Initialize` export function. More info on the [<ins>Error Message</ins>](/TygerFramework/#error-message) section on the Getting Started page

Gives more info for what went `wrong` during initialization of your plugin.

```C++
API::Get()->param()->initErrorMessage = "Write what went wrong here";
```