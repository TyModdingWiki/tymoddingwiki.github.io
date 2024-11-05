# Camera

The `Camera` class provides static methods for managing the camera's state, position, rotation, and various configuration settings in the game environment. These methods allow for getting and setting camera properties, enabling precise control over the player's view and experience.

---

## `getCameraState`

```cpp
static CameraState getCameraState();
```

Retrieves the current state of the camera.

**Returns:**

- `CameraState`: The current camera state.

---

## `setCameraState`

```cpp
static void setCameraState(CameraState state);
```

Sets the state of the camera to a specified `CameraState`.

**Parameters:**

  - `CameraState state`: The new state to apply to the camera.

---

## `getCameraPosition`

```cpp
static Vector3f getCameraPosition();
```

Returns the camera’s current position in the game world.

**Returns:**

  - `Vector3f`: A vector representing the camera's position in 3D space.

---

## `setCameraPosition`

```cpp
static void setCameraPosition(Vector3f position);
```

Sets the camera’s position to a specified 3D coordinate.

**Parameters:**

  - `Vector3f position`: The new position for the camera.

---

## `getCameraRotation`

```cpp
static Vector3f getCameraRotation();
```

Retrieves the camera’s current rotation.

**Returns:**

  - `Vector3f`: A vector representing the camera's rotation in 3D space.

---

## `setCameraRotation`

```cpp
static void setCameraRotation(Vector3f rotation);
```

Sets the camera's rotation to a specified orientation.

**Parameters:**

  - `Vector3f rotation`: The new rotation for the camera.

---

## `getFreeCamSpeed`

```cpp
static float getFreeCamSpeed();
```

Retrieves the current speed of the free camera mode, useful for controlling the camera's movement rate.

**Returns:**

  - `float`: The speed of the free camera.

---

## `setFreeCamSpeed`

```cpp
static void setFreeCamSpeed(float speed = 0.6f);
```

Sets the speed of the free camera mode.

**Parameters:**

  - `float speed`: The new speed for the free camera (default is 0.6f).

---

## `getCameraDistance`

```cpp
static float getCameraDistance();
```

Returns the current distance between the camera and the target.

**Returns:**

  - `float`: The distance from the camera to the target.

---

## `setCameraDistance`

```cpp
static void setCameraDistance(float distance);
```

Sets the camera’s distance from its target.

**Parameters:**

  - `float distance`: The new distance for the camera from its target.

---

## `setCameraDistanceValue`

```cpp
static void setCameraDistanceValue(CameraDistanceLevel level, float distance);
```

Sets the camera distance at a specific `CameraDistanceLevel`, such as low, mid, or high.

**Parameters:**

  - `CameraDistanceLevel level`: The preset distance level (e.g., `LOW`, `MID`, or `HIGH`).
  - `float distance`: The distance value for the specified level.

---

## `setCameraGoof`

```cpp
static void setCameraGoof(float value = 1.0);
```

Sets the cameras "goof" value. Just try it and enjoy :)

**Parameters:**

  - `float value`: The goof value for the camera (default is 1.0).