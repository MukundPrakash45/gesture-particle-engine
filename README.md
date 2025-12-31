# Gesture-Controlled Volumetric Particle System

![License](https://img.shields.io/badge/license-MIT-blue.svg) ![Three.js](https://img.shields.io/badge/Three.js-r128-black) ![MediaPipe](https://img.shields.io/badge/MediaPipe-Hands-orange)

## 📖 Overview

This project implements a real-time, interactive 3D visualization engine that bridges **Computer Vision (CV)** and **WebGL**. By leveraging Google's MediaPipe framework for high-fidelity hand tracking, the system translates physical spatial data into a 3D coordinate system.

The core rendering engine, built on Three.js, manages a particle cloud that dynamically morphs between parametric geometries (e.g., spheres, toroidal structures, cardioids) based on user gestures. The result is a seamless, low-latency interface where physical movement directly manipulates digital matter.



## ⚡ Key Features

* **Computer Vision Integration:** Utilizes MediaPipe Hands to detect 21 3D hand landmarks in real-time.
* **Volumetric Morphing:** Algorithms transform particle arrays between distinct mathematical states:
    * **Sphere:** Uniform distribution via spherical coordinates.
    * **Cardioid (Heart):** Parametric equation mapping.
    * **Planetary System:** Composite geometry (Central sphere + planar ring).
    * **Toroidal Helix:** Twisted mathematical curves.
* **State Machine Logic:**
    * **Tracking State:** Particles utilize linear interpolation (Lerp) to follow hand coordinates with calculated noise/drag.
    * **Expansion State (Open Hand):** Disperses particles using Perlin-like noise for an "excited" gaseous effect.
    * **Cohesion State (Fist):** Collapses particles into the target geometry and triggers state transitions.
* **Optimized Rendering:** Handles 8,000+ individual points using `BufferGeometry` and vertex coloring for maximum GPU throughput.

## 🛠️ Technical Architecture

The application operates on a continuous render loop:

1.  **Input:** The webcam feed is processed frame-by-frame by the MediaPipe ML model.
2.  **Normalization:** Hand coordinates $(x, y)$ are normalized and mapped to the Three.js World Space $(x, y, z)$.
3.  **Heuristics:** Euclidean distance between specific landmarks (Index Tip vs. Wrist) determines the "Gesture State" (Open vs. Closed).
4.  **Simulation:** Particle positions are updated physically using vector arithmetic, blending target shape data with interaction offsets.
5.  **Render:** The WebGL renderer draws the scene with additive blending for visual depth.

## 🚀 Installation & Usage

Due to CORS (Cross-Origin Resource Sharing) policies regarding webcam access and ES6 module loading, this application requires a local HTTP server.

### Prerequisites
* Python 3.x OR Node.js
* A modern browser with WebGL support (Chrome/Edge/Firefox)

### Method 1: Python (Recommended)
Run the following command in the project root directory:

```bash
# For Python 3
python -m http.server 8000
