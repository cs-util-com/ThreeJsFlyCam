# 3D Measurement Tool - User Guide

## 1. Overview

This guide explains how to use the interactive 3D measurement tool. The process involves two main workflows:
1.  **Placing Reference Points:** Mark specific locations in the 3D scene. These points are persistent and can be used for various purposes.
2.  **Creating Measurements:** Draw lines and calculate distances, path lengths, or areas by connecting previously placed reference points.

You can perform these actions while navigating freely in the 3D view.

## 2. Stage 1: Placing Reference Points

*   **Goal:** Mark specific, reusable locations in the 3D scene.
*   **Action:** While navigating (mouse locked), aim the central crosshair at a surface and **left-click**.
*   **Result:** A small white sphere appears at the clicked location, marking a persistent reference point. Place as many reference points as needed. These points remain until explicitly cleared.

## 3. Stage 2: Creating Measurements

Once you have placed reference points, you can create measurements between them.

### 3.1. Starting a Measurement

*   **Goal:** Begin measuring a distance, path, or area.
*   **Action:** Aim the crosshair at an existing reference point (white sphere) and **left-click**.
*   **Result:** This point becomes the starting point for your current measurement sequence. A colored preview line will appear, following your crosshair as you look around.

### 3.2. Measuring Distances (Single Segment)

*   **Goal:** Measure the straight-line distance between two reference points.
*   **Action:** After selecting the starting reference point, aim at a second reference point and **left-click**.
*   **Result:** A colored line appears connecting the two selected points. A label appears at the middle of the line showing the calculated distance. Each new measurement sequence uses a different color. The measurement is automatically finished after the second point is selected.

### 3.3. Measuring Paths (Polylines)

*   **Goal:** Measure the total length of a path connecting multiple reference points.
*   **Action:**
    1.  Select the starting reference point (**left-click**).
    2.  Select the next reference point in the path (**left-click**). A segment is drawn.
    3.  Select subsequent reference points (**left-click** on each).
*   **Result:** Each click on a reference point adds it to the path, creating a new colored line segment connected to the previous point. Each segment shows its individual distance. All segments in the current path measurement share the same color.

### 3.4. Finishing a Path Measurement

*   **Goal:** Finalize the current path measurement *without* closing it into an area.
*   **Action:** Press the **Enter** or **ESC** key while actively adding points to a measurement path.
*   **Result:**
    *   The measurement sequence is completed. The preview line disappears. The path remains as drawn.

### 3.5. Measuring Area (Closing a Shape)

*   **Goal:** Measure the surface area of a shape defined by connecting reference points.
*   **Action:** While creating a path (after selecting at least two points), **click** the *first* reference point of the current sequence again. The system detects that this point is already part of the sequence.
*   **Result:**
    *   The path automatically snaps closed, forming a polygon connecting the selected reference points.
    *   An "Area:" label appears near the center of the shape, showing the calculated area.
    *   The measurement is automatically finished.

### 3.6. Using the Live Preview

*   **Goal:** See the potential next segment and its distance before selecting the next point.
*   **Action:** After selecting the first point of a measurement sequence, simply aim the crosshair at another reference point (so the raycast hits the reference point sphere).
*   **Result:** A dashed line appears from the last selected reference point to the targeted reference point. A label on this dashed line shows the potential distance in real-time.

### 3.7. Snapping for Precision (Axis Lock during Measurement)

*   **Goal:** Draw measurement lines that are perfectly aligned with the scene's X, Y, or Z axes, even if the target reference point isn't directly along that axis from the previous point.
*   **Action:** *After* selecting the previous point in your measurement sequence, but *before* selecting the next reference point, press an **Arrow Key**:
    *   **Left Arrow:** Lock the next segment(s) to the X-axis direction.
    *   **Right Arrow:** Lock the next segment(s) to the Z-axis direction. (Note: Right arrow for Z-axis)
    *   **Up/Down Arrow:** Lock the next segment(s) to the Y-axis direction.
*   **Result:**
    *   When you then **left-click** on the target reference point, the tool will draw one, two, or three connected line segments between the previous point and the target point, following only the specified axis/axes.
    *   For example, connecting point A to point B using Y-axis snapping might draw a vertical line from A, then a horizontal line (along X or Z) to reach the same horizontal plane as B, and finally another vertical line to B (if needed).
    *   Intermediate points where the axis-aligned segments connect might be visually implied.
    *   Each created segment will have its own distance label.
    *   Axis snapping is active only for connecting the *next* two selected points and turns off automatically afterwards. You can press an arrow key again before selecting the subsequent point if needed.

### 3.8. Setting a Scale (Reference Measurement)

*   **Goal:** Calibrate all measurements based on a known real-world distance.
*   **Action:** **Click** (raycast hits) any *segment distance label* (not "Total:" or "Area:") while not currently creating a measurement.
*   **Result:**
    *   A prompt appears asking you to "Enter reference measurement value:", pre-filled with the label's current calculated value.
    *   Enter the known real-world distance for that specific segment and click OK.
    *   All measurement labels in the scene (distances, totals, areas) will update instantly based on this new scale factor.

### 3.9. Correcting Mistakes (Remove Last Segment)

*   **Goal:** Undo the addition of the most recent segment in the *current*, active measurement path.
*   **Action:** Press the **Backspace** or **Delete** key.
*   **Result:** The last line segment added, along with its distance label, is removed. You can continue the measurement from the previous point. This only affects the measurement you are actively working on.

### 3.10. Clearing Your Work

*   **Goal:** Remove previously placed (points) or (measurement lines and labels).
*   **Actions:**
    *   Click the **"Clear Reference Points"** button: Removes *all* white spheres (reference points). Does *not* remove measurement lines/labels. Asks for confirmation first.
    *   Click the **"Clear Measurements"** button: Removes *all* colored lines and labels (distances, totals, areas). Does *not* remove the white spheres (reference points). Asks for confirmation first.
*   **Result:** The selected items are removed from the scene. Any measurement currently in progress is cancelled.

## 4. Controls Summary

*   **Place Reference Point:** Left-click on a surface (raycast hit)
*   **Start Measurement / Add Point:** Left-click on an existing Reference Point
*   **Axis Snap (while measuring, before next point):** Arrow Keys (Left=X, Right=Z, Up/Down=Y)
*   **Set Scale:** Double-click on a segment distance label (when not measuring)
*   **Remove Last Measurement Segment (while measuring):** Backspace / Delete
*   **Finish Path Measurement (Open):** Enter / ESC (while measuring)
*   **Finish Area Measurement (Closed):** Left-click on the *first* point of the current measurement (while measuring)
*   **Clear All Points:** "Clear Reference Points" button
*   **Clear All Measurements:** "Clear Measurements" button

## 5. Visual Cues

*   **Reference Points:** Small white spheres.
*   **Measurement Lines:** Colored lines connecting selected reference points. Different colors for different measurement sequences. Axis snapping may create multiple connected segments between two selected points.
*   **Preview Line:** A dashed colored line from the last point to the crosshair's target reference point, showing the potential next segment and distance.
*   **Labels:** Show calculated values (distance, total length, area) in white text on colored backgrounds matching the lines. Labels always face the camera.
