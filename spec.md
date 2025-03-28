## **Specification: 3D Scene Navigation (Third-Person Fly-Through)**

**1\. Overview & Goal**

This specification details the requirements for implementing a third-person, "fly-through" navigation system within a 3D scene. The user should experience smooth, intuitive control similar to a third-person space shooter or drone simulation, using standard keyboard and mouse inputs. The primary goal is to allow free exploration of the 3D space for initial UX evaluation, with a specific focus on the camera movement and aiming mechanics. This system will serve as the foundation for future interactions, such as measurement tools.

**2\. Target Platform & Technology**

* **Platform:** Modern Web Browsers supporting WebGL.  
* **Architecture:** Single Page Application (SPA).  
* **Core Library:** Three.js.

**3\. Core Features**

* Third-person camera perspective.  
* Fly-through movement using WASD or Arrow keys.  
* Mouse-look rotation around a central pivot point without requiring clicking/dragging.  
* Movement speed boost modifier (Shift key).  
* Adjustable parameters for key aspects (speed, sensitivity, camera distance).  
* Visible crosshair centered on the screen.

**4\. Scene Setup**

* **Purpose:** Provide a basic environment for testing navigation UX.  
* **Content:**  
  * A flat ground plane (e.g., a large PlaneGeometry with a basic material).  
  * Several simple geometric shapes (e.g., cubes, spheres, cones using BoxGeometry, SphereGeometry, ConeGeometry) placed at various positions and scales on or above the ground plane to provide visual cues for movement and orientation.  
*   
* **Interaction:** Scene elements are purely visual; no collision detection or physics interaction is required for this phase.

**5\. Initial State & Camera Setup**

* **Camera Type:** THREE.PerspectiveCamera.  
* **Initial Camera Position:** Positioned behind the central pivot point. The distance behind the pivot is defined by the initialCameraDistance constant.  
* **Initial Pivot Point Position:** Located initialCameraDistance directly in front of the camera along its forward vector.  
* **Initial Camera Orientation:** Looking straight ahead, parallel to the ground plane (horizontal view). The camera should target the pivot point initially, but its view direction vector should be parallel to the ground.  
* **Field of View (FOV):** Use a standard FOV suitable for comfortable viewing (e.g., 75 degrees), potentially making this another adjustable constant if needed later.

**6\. Control Mapping & Behavior**

| Input | Action | Behavior |
| :---- | :---- | :---- |
| **Mouse Move X** | Rotate View Horizontally | Rotates the camera horizontally around the central pivot point. The pivot point's world position remains the same during rotation, only the camera position changes relative to it. |
| **Mouse Move Y** | Rotate View Vertically | Rotates the camera vertically around the central pivot point. The pivot point's world position remains the same during rotation, only the camera position changes relative to it. |
| **W / Up Arrow** | Move Forward | Moves both the camera and the central pivot point forward together along the camera's current view direction (parallel to the ground if looking horizontally). |
| **S / Down Arrow** | Move Backward | Moves both the camera and the central pivot point backward together along the camera's current view direction. |
| **A / Left Arrow** | Strafe Left | Moves both the camera and the central pivot point sideways to the left, perpendicular to the camera's current view direction. |
| **D / Right Arrow** | Strafe Right | Moves both the camera and the central pivot point sideways to the right, perpendicular to the camera's current view direction. |
| **Shift (Hold)** | Activate Boost Speed | While held down in conjunction with W, A, S, or D (or Arrow keys), increases movement speed according to boostMoveSpeed. |
| **Left Click** | *(Reserved)* | No action defined in this specification. Reserved for future measurement UX. |

**7\. Movement Logic**

* **Mechanism:** Update the world position of the central pivot point based on key inputs and the camera's current orientation vectors (forward and right vectors).  
* **Camera Following:** The camera's position should be updated to always maintain the initialCameraDistance distance behind the pivot point along the camera's negative view vector.  
* **Speed:**  
  * Default movement speed: normalMoveSpeed.  
  * Boosted movement speed (Shift held): boostMoveSpeed.  
*   
* **Responsiveness:** Movement should start and stop instantly upon key press/release. No acceleration, deceleration, or inertia.  
* **Coordinate System:** Use the camera's local coordinate system to determine "forward", "backward", and "sideways" directions for movement relative to the current view.  
* **Collision:** No collision detection. Movement is unrestricted by the scene geometry or ground plane.

**8\. Rotation Logic**

* **Mechanism:** Use mouse movement delta (change in X and Y position between frames) to calculate rotation angles.  
* **Pivot:** Rotation occurs around the central pivot point. The pivot point's world coordinates do not change during a pure rotation action; only the camera's position relative to the pivot changes, orbiting it.  
* **Sensitivity:** Apply the mouseSensitivity constant to scale mouse movement delta into rotation angles (e.g., radians). A single constant applies to both horizontal and vertical rotation.  
* **Vertical Limits:** Clamp the vertical rotation (pitch) between \-90 degrees (looking straight down) and \+90 degrees (looking straight up). This prevents gimbal lock issues and maintains orientation.  
* **Horizontal Limits:** No limits on horizontal rotation (yaw).  
* **Responsiveness:** Rotation should respond instantly to mouse movement. No mouse smoothing or acceleration.  
* **Implementation Note:** Consider using Euler angles or Quaternions for managing rotation in Three.js. Quaternions are generally preferred to avoid gimbal lock, though careful Euler order application might suffice given the \+/- 90-degree vertical clamp. The camera should always lookAt the pivot point after its position is updated based on rotation.

**9\. Crosshair Implementation**

* **Appearance:** A small, white dot.  
* **Position:** Fixed permanently in the exact center of the viewport/canvas.  
* **Size:** Fixed diameter defined by crosshairSize (in pixels).  
* **Implementation:** Draw using HTML/CSS overlayed on the canvas, or using an OrthographicCamera setup in Three.js to render screen-space elements. HTML/CSS overlay is likely simpler.

**10\. Configuration / Adjustable Constants**

The following parameters should be easily configurable (e.g., defined as constants near the top of the relevant code file or in a configuration object) to allow for tweaking and tuning the UX:

| Constant Name | Description | Initial Value | Unit |
| :---- | :---- | :---- | :---- |
| initialCameraDistance | Distance from camera to the central pivot point. | 10 | meters |
| normalMoveSpeed | Base movement speed. | 1 | meters/second |
| boostMoveSpeed | Movement speed when Shift key is held. | 2 | meters/second |
| mouseSensitivity | Factor converting mouse movement to rotation. | *(Needs TBD)* | units/pixel |
| crosshairSize | Diameter of the crosshair dot. | 2 | pixels |

*(Note: An appropriate starting value for mouseSensitivity will need experimentation, e.g., 0.002)*

**11\. Architecture Considerations**

* **Input Handling:** Implement event listeners for keydown, keyup, and mousemove. Capture mouse movement delta rather than absolute position. Consider using the Pointer Lock API (requestPointerLock) for a smoother FPS-like mouse experience where the cursor is hidden and doesn't hit screen edges (optional but recommended for this control style).  
* **Update Loop:** Integrate camera position/rotation updates within the main Three.js animation loop (requestAnimationFrame). Calculate movement/rotation based on elapsed time since the last frame to ensure frame-rate independence.  
* **State Management:** Maintain the current state of pressed keys (W, A, S, D, Shift) to handle continuous movement.

**12\. Data Handling**

* **Scene Data:** The application will load/create the Three.js scene graph (ground plane, geometric shapes). For this phase, this data is static and purely visual.  
* **User Input Data:** Mouse movement delta (dx, dy) and keyboard state are the primary input data points.

**13\. Error Handling**

* **WebGL Support:** Check for WebGL availability in the user's browser and display an appropriate message if unavailable.  
* **Pointer Lock API:** If used, handle cases where the user denies pointer lock permission or the browser doesn't support it. Provide fallback behavior (standard mouse move events) if necessary, though the experience might be slightly degraded.  
* **Input Focus:** Ensure the canvas or relevant DOM element has focus to receive keyboard events.

**14\. Testing Plan**

* **Initial State:** Verify camera position, orientation (looking horizontally), and distance from pivot point upon loading. Verify the crosshair is centered and visible.  
* **Movement (WASD/Arrows):**  
  * Press W/Up: Confirm forward movement along view direction.  
  * Press S/Down: Confirm backward movement along view direction.  
  * Press A/Left: Confirm strafe left movement perpendicular to view.  
  * Press D/Right: Confirm strafe right movement perpendicular to view.  
  * Hold Shift \+ WASD: Confirm movement speed increases.  
  * Test movement in various camera orientations (looking up, down, sideways).  
  * Verify movement stops instantly on key release.  
*   
* **Rotation (Mouse):**  
  * Move mouse left/right: Confirm smooth horizontal rotation around the pivot.  
  * Move mouse up/down: Confirm smooth vertical rotation around the pivot.  
  * Test vertical limits: Confirm view clamps at straight up (+90deg) and straight down (-90deg) and doesn't flip.  
  * Verify rotation feels direct and responsive.  
*   
* **Crosshair:** Confirm the crosshair remains fixed in the center of the viewport during all movement and rotation.  
* **No Collision:** Verify the camera can pass through the ground plane and geometric shapes freely.  
* **Constants:** Temporarily modify adjustable constants (initialCameraDistance, speeds, sensitivity, crosshairSize) and verify the changes take effect in the application's behavior.  
* **Browser Compatibility:** Test in target browsers (e.g., Chrome, Firefox, Safari, Edge).

**15\. Future Considerations (Out of Scope for this Spec)**

* Implementation of the measurement UX triggered by a left mouse click using the crosshair for aiming.  
* More complex scene loading.  
* Advanced graphics features (lighting, shadows, textures).  
* User configuration UI for sensitivity, speed, etc.  
* Collision detection and response.