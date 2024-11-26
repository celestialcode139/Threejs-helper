# Threejs Helper

This module provides utilities for setting up and managing a Three.js scene. It includes functions for creating scenes, handling user interactions, loading models, and integrating advanced features like raycasting and observers.

## Modules and Dependencies

The module uses the following libraries:
- `three`
- `three/examples/jsm/loaders/GLTFLoader`
- `three/examples/jsm/loaders/DRACOLoader`
- `three/examples/jsm/loaders/KTX2Loader`
- `three/addons/controls/OrbitControls.js`
- `three/addons/libs/stats.module.js`
- `meshoptimizer`

---

## Global Variables
The following variables are initialized and used globally:
- **scene**: Three.js Scene object.
- **camera**: Three.js PerspectiveCamera.
- **renderer**: Three.js WebGLRenderer.
- **debug**: Enables or disables debugging features.
- **orbit**: OrbitControls instance.
- **axis**: AxesHelper for visualization.
- **grid**: GridHelper for visualization.
- **stats**: Stats module for performance monitoring.
- **raycaster**: Raycaster instance for detecting intersections.
- **pointer**: Vector2 for pointer position.
- **previouslyHovered**: Tracks previously hovered objects during raycasting.

---

## Functions

### `createScene({canvas:canvas},{ fov: 75, near: 0.1, far: 1000 },true)`
Creates and initializes a Three.js scene.

- **Parameters:**
  - `webglparams` (Object): WebGLRenderer parameters.
  - `cameraparams` (Object): Camera parameters (`fov`, `near`, `far`).
  - `debuger` (Boolean): Enables debugging features.
  
- **Returns:**
  - `{ scene, camera, renderer, orbit }`

---

### `Tcontrol(mesh)`
Adds TransformControls to manipulate a mesh in the scene.

- **Parameters:**
  - `mesh` (Object): The mesh to be controlled.

---

### `Model(path)`
Loads a GLTF model.

- **Parameters:**
  - `path` (String): Path to the GLTF model.

- **Returns:**
  - `Promise` resolving to the loaded GLTF object.

---

### `HDRMap(hdr)`
Loads an HDR environment map.

- **Parameters:**
  - `hdr` (String): Path to the HDR file.

---

### `CubeTexture(path)`
Loads a cube texture for environment and background.

- **Parameters:**
  - `path` (String): Path to the texture files (base path).

---

### `Observer(sectionClass, cbin, cbout)`
Creates an intersection observer for DOM elements.

- **Parameters:**
  - `sectionClass` (String): Class of the sections to observe.
  - `cbin` (Function): Callback when the section comes into view.
  - `cbout` (Function): Callback when the section goes out of view.

---

### `Monitor()`
Adds a performance monitoring overlay using `Stats`.

---

### `Raycast(cb)`
Sets up raycasting to detect intersections in the scene.

- **Parameters:**
  - `cb` (Function): Callback for handling intersections.

---

## Utilities

### Key Bindings (Debug Mode)
- **`o`**: Toggle OrbitControls.
- **`a`**: Toggle AxesHelper visibility.
- **`g`**: Toggle GridHelper visibility.
- **`q`**: Toggle TransformControls between `local` and `world` space.
- **`Shift`**: Enable snapping for TransformControls.
- **`w`**: Switch TransformControls to translation mode.
- **`e`**: Switch TransformControls to rotation mode.
- **`r`**: Switch TransformControls to scaling mode.
- **`+` / `=`**: Increase TransformControls size.
- **`-` / `_`**: Decrease TransformControls size.
- **`x`**: Toggle visibility of the X-axis handle.
- **`y`**: Toggle visibility of the Y-axis handle.
- **`z`**: Toggle visibility of the Z-axis handle.
- **`Space`**: Enable/disable TransformControls.
- **`Escape`**: Reset TransformControls.

---

## Example Usage

```javascript
import { createScene, model, Tcontrol, HDRMap } from './MyThreeComponent';

// Initialize the scene
const { scene, camera, renderer } = createScene({ antialias: true }, { fov: 60 });

// Load a model
model('./path/to/model.gltf').then((gltf) => {
  scene.add(gltf.scene);
});

// Add HDR environment
HDRMap('./path/to/environment.hdr');

// Start rendering loop
function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}
animate();
