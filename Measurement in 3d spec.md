# 3D Measurement Tool Specification

## 1. Overview

This document outlines the specifications for an interactive 3D measurement tool integrated within a Three.js scene utilizing fly navigation controls. The tool allows users to measure distances, polylines, and areas directly within the 3D environment.

## 2. Core Features

### 2.1. Point Placement

*   **Action:** Left-click in the 3D view while pointer-locked.
*   **Behavior:**
    *   A raycast originates from the center of the screen (crosshair).
    *   If the ray intersects an existing scene object (excluding measurement objects) or a previously placed reference point, a new measurement point is created at the intersection.
    *   If no intersection occurs, a point is placed along the camera's view direction at a default distance (e.g., 5 units) from the last placed point or camera position if it's the first point.
    *   Placed points are visualized as small white spheres (e.g., `SphereGeometry(0.05, 8, 8)`).
    *   Points are added to the `measurementGroup` and tracked in `measurementObjects.points`.

### 2.2. Line Segment Creation

*   **Action:** Placing a second point after a first point has been placed.
*   **Behavior:**
    *   A solid line segment is drawn between the last two placed points.
    *   The line uses a color from a predefined pastel palette (`lineColors`), cycling through the palette for each new measurement sequence.
    *   A text label (Sprite) is created at the midpoint of the segment, displaying the calculated distance between the two points.
    *   The distance displayed on the label is affected by the `globalScaleFactor`.
    *   The label background and border color match the line color.
    *   Lines and labels are added to the `measurementGroup` and tracked in `measurementObjects.lines` and `measurementObjects.labels`.

### 2.3. Polyline Measurement

*   **Action:** Placing three or more points consecutively before completing the measurement.
*   **Behavior:**
    *   Each new point creates a new line segment connected to the previous point.
    *   All segments within the current measurement sequence share the same color.
    *   Individual segment distances are displayed.

### 2.4. Measurement Completion

*   **Action:** Pressing `Enter` or `R` key.
*   **Behavior:**
    *   Finalizes the current measurement sequence (polyline or single segment).
    *   Removes the preview line and label.
    *   If the sequence contains more than two points (i.e., a polyline), a "Total:" label is created near the center of the polyline, displaying the sum of all segment distances in that sequence. The total distance is affected by the `globalScaleFactor`.
    *   The system prepares for a new measurement sequence, selecting the next color from the palette.
    *   If only one point was placed, the measurement is cancelled.

### 2.5. Loop Closure and Area Calculation

*   **Action:** Placing a point very close (within a small threshold, e.g., 0.01 units) to the *first* point of the current measurement sequence (requires at least 3 points placed).
*   **Behavior:**
    *   The last placed point snaps exactly to the position of the first point, closing the loop.
    *   The surface area of the resulting polygon is calculated using Newell's method.
    *   An "Area:" label is created near the center of the polygon, displaying the calculated area. The area is affected by the square of the `globalScaleFactor`.
    *   The measurement sequence is automatically completed.

### 2.6. Preview Visualization

*   **Behavior:**
    *   When at least one point has been placed in the current sequence, a dashed preview line is drawn from the last placed point to the current crosshair intersection point (or a point along the view direction if no intersection).
    *   A preview distance label is displayed at the midpoint of the dashed line.
    *   The preview line and label update in real-time as the user looks around.
    *   The preview line and label use the color assigned to the current measurement sequence.

### 2.7. Axis Snapping

*   **Action:** Pressing Arrow Keys (`Up/Down` for Y, `Left` for X, `Right` for Z) before placing the *next* point.
*   **Behavior:**
    *   Activates snapping mode for the specified axis (`x`, `y`, or `z`).
    *   When placing the next point, its position will be constrained to share the selected axis coordinate(s) with the *previous* point.
        *   X-Snap: New point's Y and Z match the previous point's Y and Z.
        *   Y-Snap: New point's X and Z match the previous point's X and Z.
        *   Z-Snap: New point's X and Y match the previous point's X and Y.
    *   The preview line and point visualization update to reflect the snapping constraint.
    *   Snapping is deactivated after the point is placed.

### 2.8. Point Snapping

*   **Behavior:**
    *   When placing a point, if the raycast intersects an existing reference point sphere, the new point snaps exactly to the center of that existing point.

### 2.9. Reference Measurement and Scaling

*   **Action:** Double-clicking on a segment distance label (not a "Total:" or "Area:" label).
*   **Behavior:**
    *   Pointer lock is released (if active).
    *   A prompt appears, asking the user to "Enter reference measurement value:", pre-filled with the label's current text.
    *   If the user enters a valid number:
        *   The `globalScaleFactor` is recalculated based on the ratio of the entered value to the segment's *original* measured distance (before scaling). `globalScaleFactor = newValue / originalDistance`.
        *   All existing measurement labels (segment distances, total distances, areas) are updated immediately to reflect the new `globalScaleFactor`. Areas are scaled by the factor squared.
*   **Initial State:** `globalScaleFactor` defaults to `1.0`.

### 2.10. Removing Points

*   **Action:** Pressing `Backspace` or `Delete` key.
*   **Behavior:**
    *   Removes the last placed point in the *current* measurement sequence.
    *   Removes the associated line segment and distance label connected to that point.
    *   Updates the preview line to originate from the new last point.
    *   Does not affect completed measurements or reference points not part of the active measurement.

### 2.11. Clearing Data

*   **Clear Reference Points Button:**
    *   Prompts the user for confirmation.
    *   Removes *all* placed reference point spheres from the scene and internal tracking.
    *   If a measurement is in progress, it is cancelled.
*   **Clear Measurements Button:**
    *   Prompts the user for confirmation.
    *   Removes *all* measurement lines and labels (segment, total, area) from the scene and internal tracking.
    *   Does *not* remove reference point spheres.
    *   If a measurement is in progress, it is cancelled.

## 3. User Controls Summary

*   **Left Mouse Click:**
    *   If pointer not locked: Request pointer lock.
    *   If pointer locked: Place measurement point.
*   **Double Left Mouse Click:** (On a distance label) Initiate reference measurement editing.
*   **Arrow Keys (Up/Down/Left/Right):** Activate axis snapping for the next point (Y/Y/X/Z).
*   **Backspace / Delete:** Remove the last point of the current measurement.
*   **Enter / R:** Complete the current measurement sequence.
*   **ESC:** Release pointer lock.

## 4. Visual Style

*   **Reference Points:** Small, solid white spheres.
*   **Measurement Lines:** Solid lines using a cycling palette of pastel colors (e.g., Mint, Pink, Orange, Blue...).
*   **Preview Line:** Dashed line using the color of the current measurement sequence.
*   **Labels:**
    *   Rendered as `THREE.Sprite` using `CanvasTexture`.
    *   Display text (distance, total, area) in white font.
    *   Background color is a slightly darker shade of the corresponding line color with some transparency.
    *   Border color matches the corresponding line color.
    *   Labels always face the camera.
    *   Rendered on top of other scene elements (`renderOrder = 999`, `depthTest = false`).

## 5. Technical Details

*   All measurement objects (points, lines, labels) are added to a dedicated `THREE.Group` (`measurementGroup`) for easier management.
*   Raycasting (`THREE.Raycaster`) is used for point placement and label interaction.
*   State is managed in `measurementState` and `measurementObjects` objects.
*   Uses a predefined list of hex color codes (`lineColors`) for measurement sequences.
