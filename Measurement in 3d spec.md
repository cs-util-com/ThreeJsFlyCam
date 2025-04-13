# 3D Measurement Tool - User Guide

## 1. Overview

This guide explains how to use the interactive 3D measurement tool. You can measure distances between points, the length of multi-segment paths (polylines), and the area of closed shapes directly within the 3D view while navigating freely.

## 2. How to Measure

### 2.1. Marking Points

*   **Goal:** Mark specific locations in the 3D scene to start measuring.
*   **Action:** While navigating (mouse locked), aim the central crosshair at a surface or an existing measurement point and **left-click**.
*   **Result:** A small white sphere appears at the location you clicked, marking your first measurement point. If you click in empty space, a point is placed a short distance in front of you.

### 2.2. Measuring Distances (Single Segment)

*   **Goal:** Measure the straight-line distance between two points.
*   **Action:** After placing your first point, aim and **left-click** again to place a second point.
*   **Result:** A colored line appears connecting the two points. A label appears at the middle of the line showing the calculated distance. Each new measurement sequence will use a different color.

### 2.3. Measuring Paths (Polylines)

*   **Goal:** Measure the total length of a path made of multiple connected segments.
*   **Action:** Place three or more points consecutively by **left-clicking** for each point.
*   **Result:** Each click adds a new point and a new colored line segment connected to the previous point. Each segment shows its individual distance. All segments in the current path measurement share the same color.

### 2.4. Finishing a Measurement

*   **Goal:** Finalize the current distance or path measurement.
*   **Action:** Press the **Enter** or **R** key.
*   **Result:**
    *   The temporary preview line disappears.
    *   If you measured a path (3+ points), a "Total:" label appears near the path's center, showing the sum of all segment lengths.
    *   The tool is ready for you to start a new measurement with a new color.
    *   If you only placed one point, the measurement is cancelled.

### 2.5. Measuring Area (Closing a Shape)

*   **Goal:** Measure the surface area of a flat shape you draw.
*   **Action:** While creating a path (after placing at least two points), place the *next* point very close to your *first* point in the current sequence.
*   **Result:**
    *   The path automatically snaps closed, forming a polygon.
    *   An "Area:" label appears near the center of the shape, showing the calculated area.
    *   The measurement is automatically finished.

### 2.6. Using the Live Preview

*   **Goal:** See the potential next segment and its distance before clicking.
*   **Action:** After placing at least one point, simply look around.
*   **Result:** A dashed line appears from your last placed point to where your crosshair is aiming. A label on this dashed line shows the distance in real-time. This helps you position the next point accurately.

### 2.7. Snapping for Precision (Axis Lock)

*   **Goal:** Place the next point perfectly aligned horizontally or vertically with the previous point.
*   **Action:** *Before* placing the next point, press an **Arrow Key**:
    *   **Left Arrow:** Lock to the X-axis (aligns Y and Z coordinates).
    *   **Right Arrow:** Lock to the Z-axis (aligns X and Y coordinates).
    *   **Up/Down Arrow:** Lock to the Y-axis (aligns X and Z coordinates).
*   **Result:** The preview line and point will jump to the snapped position. The next **left-click** will place the point on that axis. Snapping turns off automatically after the click.

### 2.8. Snapping to Existing Points

*   **Goal:** Connect precisely to a point you've already placed.
*   **Action:** Aim the crosshair directly at an existing white sphere (measurement point) and **left-click**.
*   **Result:** The new point snaps exactly to the center of the existing point.

### 2.9. Setting a Scale (Reference Measurement)

*   **Goal:** Calibrate all measurements based on a known real-world distance.
*   **Action:** **Double-click** on any *segment distance label* (not "Total:" or "Area:").
*   **Result:**
    *   Navigation pauses (mouse is released).
    *   A prompt appears asking you to "Enter reference measurement value:", pre-filled with the label's current value.
    *   Enter the known real-world distance for that segment and click OK.
    *   All measurement labels in the scene (distances, totals, areas) will update instantly based on this new scale.

### 2.10. Correcting Mistakes (Remove Last Point)

*   **Goal:** Undo the placement of the most recent point in the *current* measurement.
*   **Action:** Press the **Backspace** or **Delete** key.
*   **Result:** The last point placed, along with its connecting line and label, is removed. You can continue measuring from the previous point. This only affects the measurement you are actively working on.

### 2.11. Clearing Your Work

*   **Goal:** Remove previously placed points or measurement lines/labels.
*   **Actions:**
    *   Click the **"Clear Reference Points"** button: Removes *all* the white spheres (points) you've placed. Asks for confirmation first.
    *   Click the **"Clear Measurements"** button: Removes *all* the colored lines and labels (distances, totals, areas). Does *not* remove the white spheres. Asks for confirmation first.
*   **Result:** The selected items are removed from the scene. Any measurement in progress is cancelled.

## 3. Controls Summary

*   **Navigate:** WASD (Move), Shift (Boost), Mouse (Look), ESC (Release Mouse)
*   **Start Navigation / Place Point:** Left-click
*   **Set Scale:** Double-click on a distance label
*   **Axis Snap (Before Clicking):** Arrow Keys (Left=X, Right=Z, Up/Down=Y)
*   **Remove Last Point:** Backspace / Delete
*   **Complete Measurement:** Enter / R
*   **Clear Points:** "Clear Reference Points" button
*   **Clear Lines/Labels:** "Clear Measurements" button

## 4. Visual Cues

*   **Points:** Small white spheres mark locations.
*   **Lines:** Colored lines connect points. Different colors for different measurement sequences (distance, polyline, area).
*   **Preview:** A dashed line shows where the next segment will go.
*   **Labels:** Show calculated values (distance, total length, area) in white text on colored backgrounds that match the lines. Labels always face you.
