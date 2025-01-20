# Hero 

The `Hero` class provides static methods for controlling and retrieving the state, position, and physical properties of a game character. Each method is documented below with its return types, parameters, and purpose.

---

## `setState(int state)`

```cpp
static void setState(int state);
```

Sets the hero's state using an integer identifier.

!!! warning
    This assumes the state is valid for the current hero. Providing an invalid state may cause game-breaking behaviour.

**Parameters:**

  - `int state`: The integer identifier representing the new state of the hero.

---

## `setState(BullState state)`

```cpp
static void setState(BullState state);
```

Sets the hero's state if it corresponds to the `BullState` type.

!!! warning
    This assumes the current hero is `BushPig`. Providing an invalid state may cause game-breaking behaviour.

**Parameters:**

  - `BullState state`: The new state for `BushPig`.

---

## `setState(TyState state)`

```cpp
static void setState(TyState state);
```

Sets the hero's state if it corresponds to the `TyState` type.

!!! warning
    This assumes the current hero is `Ty`. Providing an invalid state may cause game-breaking behaviour.

**Parameters:**

  - `TyState state`: The new state for `Ty`.

---

## `getState`

```cpp
static int getState();
```

Retrieves the current integer-based state of the hero. The state will be for the currently active hero. This can then be cast to either of the hero state types depending on the current hero.

!!! tip
    You can use `isBull()` to determine which hero is currently active.

**Returns:**

  - `int`: The current state of the hero.

---

## `getPosition`

```cpp
static Vector3f getPosition();
```

Returns the current position of the hero in 3D space as a `Vector3f` object.

**Returns:**

  - `Vector3f`: The current coordinates of the hero.

---

## `setPosition`

```cpp
static void setPosition(Vector3f coords);
```

Sets the hero's position to the specified coordinates.

**Parameters:**

  - `Vector3f coords`: The new 3D position of the hero.

---

## `getHealth`

```cpp
static int getHealth();
```

Retrieves the current health level of the hero. A single paw is 4 health by default.

**Returns:**

  - `int`: The hero's current health.

---

## `setHealth`

```cpp
static void setHealth(int health);
```

Sets the hero's health to the specified value. A single paw is 4 health by default.

**Parameters:**

  - `int health`: The new health value of the hero.

---

## `getBreath`

```cpp
static int getBreath();
```

Retrieves the current breath level of the hero. 

Only applies while underwater and returns `0` if the currently active hero is `BushPig`.

**Returns:**

  - `int`: The current breath level of the hero.

---

## `setBreath`

```cpp
static void setBreath(int breath);
```

Sets the hero's breath level.

Only applies while underwater and returns early if the currently active hero is `BushPig`.

**Parameters:**

  - `int breath`: The new breath value of the hero.

---

!!! Info
    Many of the setters for the movements attributes which follow have default values for their parameters meaning they can be called with no arguments to reset the values to default.

---

## `getSwimSpeed`

```cpp
static float getSwimSpeed();
```

Retrieves the hero's swimming speed.

**Returns:**

  - `float`: The swimming speed of the hero.

---

## `setSwimSpeed`

```cpp
static void setSwimSpeed(float speed = 20.0f);
```

Sets the hero's swimming speed. Default value is `20.0f`.

**Parameters:**

  - `float speed`: The new swimming speed of the hero.

---

## `getRunSpeed`

```cpp
static float getRunSpeed();
```

Retrieves the hero's running speed.

**Returns:**

  - `float`: The running speed of the hero.

---

## `setRunSpeed`

```cpp
static void setRunSpeed(float speed = 10.0f);
```

Sets the hero's running speed. Default value is `10.0f`.

**Parameters:**

  - `float speed`: The new running speed of the hero.

---

## `getAirSpeed`

```cpp
static float getAirSpeed();
```

Retrieves the hero's airborne speed.

**Returns:**

  - `float`: The air speed of the hero.

---

## `setAirSpeed`

```cpp
static void setAirSpeed(float speed = 10.0f);
```

Sets the hero's speed when airborne. Default value is `10.0f`.

**Parameters:**

  - `float speed`: The new air speed of the hero.

---

## `getJumpHeight`

```cpp
static float getJumpHeight();
```

Retrieves the hero's default jump height.

**Returns:**

  - `float`: The default jump height of the hero.

---

## `setJumpHeight`

```cpp
static void setJumpHeight(float height = 18.57f);
```

Sets the hero's jump height. Default value is `18.57f`.

**Parameters:**

  - `float height`: The new jump height of the hero.

---

## `getDoubleJumpHeight`

```cpp
static float getDoubleJumpHeight();
```

Retrieves the height for the hero's double jump.

**Returns:**

  - `float`: The double jump height.

---

## `setDoubleJumpHeight`

```cpp
static void setDoubleJumpHeight(float height = 8.37f);
```

Sets the height of the hero's double jump. Default value is `8.37f`.

**Parameters:**

  - `float height`: The new double jump height.

---

## `getLedgeGrabTolerance`

```cpp
static float getLedgeGrabTolerance();
```

Returns the tolerance level when the hero grabs a ledge.

**Returns:**

  - `float`: The ledge grab tolerance.

---

## `setLedgeGrabTolerance`

```cpp
static void setLedgeGrabTolerance(float tolerance = 20.0f);
```

Sets the hero's tolerance for ledge grabs. Default value is `20.0f`.

**Parameters:**

  - `float tolerance`: The new ledge grab tolerance.

---

## `getGlideSpeed`

```cpp
static float getGlideSpeed();
```

Retrieves the hero's gliding speed.

**Returns:**

  - `float`: The glide speed of the hero.

---

## `setGlideSpeed`

```cpp
static void setGlideSpeed(float speed = 7.0f);
```

Sets the hero's gliding speed. Default value is `7.0f`.

**Parameters:**

  - `float speed`: The new glide speed of the hero.

---

## `getGravity`

```cpp
static float getGravity();
```

Retrieves the current gravity affecting the hero.

**Returns:**

  - `float`: The gravity level affecting the hero.

---

## `setGravity`

```cpp
static void setGravity(float gravity = 0.75f);
```

Sets the gravity value for the hero. Default value is `0.75f`.

**Parameters:**

  - `float gravity`: The new gravity value.

---

## `getInvincibility`

```cpp
static bool getInvincibility();
```

Checks if the hero is invincible.

**Returns:**

  - `bool`: `true` if the hero is invincible; otherwise, `false`.

---

## `setInvincibility`

```cpp
static void setInvincibility(bool status);
```

Sets the hero's invincibility status.

**Parameters:**

  - `bool status`: `true` to make the hero invincible; `false` otherwise.

---

## `kill`

```cpp
static void kill();
```

Triggers the hero's death by setting state to `dying`. 

Automatically sets the correct state depending on the currently active hero.

---

## `setMainSkin`

```cpp
static void setMainSkin(int index);
```

Sets the hero's main skin based on an index.

This does not include the eye skin.

**Parameters:**

  - `int index`: The skin index.

---

## `resetValues`

```cpp
static void resetValues();
```

Resets all attributes of the hero to default values.

---

## `isBull`

```cpp
static bool isBull();
```

Checks if the currently active hero is `BushPig`.

**Returns:**

  - `bool`: `true` if the hero is `BushPig`; otherwise, `false`.