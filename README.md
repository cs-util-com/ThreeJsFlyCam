# Three.js 3D Fly-Through & Measurement Tool

Try it live: [https://cs-util-com.github.io/ThreeJsFlyCam/](https://cs-util-com.github.io/ThreeJsFlyCam/)

## Overview
This web app is a 3D navigation and measurement tool built with [Three.js](https://threejs.org/). It provides a third-person fly-through camera system and an interactive measurement tool for exploring and annotating 3D scenes directly in your browser.

- **Third-person fly navigation**: Move freely in 3D space using WASD and mouse look, with a visible crosshair for aiming.
- **Interactive measurement tool**: Place reference points, measure distances, paths, and areas, and calibrate measurements to real-world units.
- **Modern UI**: Built with Tailwind CSS for a clean, responsive interface.

## Features
### Navigation
- **WASD or Arrow Keys**: Move forward/back/strafe left/right
- **Mouse Look**: Rotate camera around a central pivot (no click-drag needed)
- **Shift**: Speed boost while moving
- **Scroll Wheel**: Zoom camera in/out
- **Pointer Lock**: Click the scene to enable immersive mouse look (ESC to release)
- **Crosshair**: Always centered for precise aiming

### Scene
- Several geometric shapes (boxes, spheres, cones, etc.) for navigation and measurement
- Ambient and directional lighting
- Fog and colored background for depth

### Measurement Tool
- **Place Reference Points**: Left-click to mark locations in the scene
- **Create Measurements**: Connect points to measure distances, paths, or areas
- **Live Preview**: See potential next segment and its distance before placing
- **Axis Snapping**: Use arrow keys to lock measurement segments to X, Y, or Z axes
- **Edit Scale**: Double-click a segment label to set a real-world reference distance
- **Undo**: Backspace/Delete removes the last segment while measuring
- **Finish Measurement**: Enter or R completes the current measurement; close a loop to measure area
- **Clear Buttons**: Remove all reference points or all measurements with confirmation
- **Labels**: Show distances, totals, and areas; always face the camera

## Controls Summary
| Action | Control |
|--------|---------|
| Move | WASD / Arrow Keys |
| Speed Boost | Shift (hold) |
| Look Around | Mouse Move |
| Zoom | Mouse Wheel |
| Lock/Unlock Mouse | Click canvas / ESC |
| Place Reference Point | Left-click |
| Add Measurement Point | Left-click on reference point |
| Snap to Axis | Arrow Keys (while measuring) |
| Remove Last Segment | Backspace / Delete |
| Complete Measurement | Enter / R |
| Set Scale | Double-click label |
| Clear Reference Points | Button (bottom left) |
| Clear Measurements | Button (bottom left) |

## Technical Details
- **Camera**: Perspective, orbits a pivot point, always maintains set distance
- **Movement**: Instant start/stop, no inertia, unrestricted (no collision)
- **Pointer Lock**: Uses browser Pointer Lock API for FPS-style mouse look
- **Configurable**: Camera distance, speed, sensitivity, and more are easily adjustable in code

## Development
- Single-file app: All logic is in `index.html` (uses ES modules and import maps)
- No build step required; just open in a modern browser