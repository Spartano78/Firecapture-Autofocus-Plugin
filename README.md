# **Lunar/Solar/Planetary Autofocus V2.8**

Professional multilanguage autofocus plugin for FireCapture (tested on Firecapture V. 2.7.15), developed by Stefano Romani, designed specifically for high-resolution planetary, lunar, and solar imaging with motorized focusers (e.g., Celestron via ASCOM/CPWI).

---
[![GitHub All Releases](https://img.shields.io/github/downloads/Spartano78/Firecapture-Autofocus-Plugin/total?style=flat-square&color=blue)](https://github.com/Spartano78/Firecapture-Autofocus-Plugin/releases/latest)

## **1. Plugin Installation**

To ensure FireCapture correctly recognizes and loads the plugin at startup, follow this exact folder structure:

1. Navigate to your main FireCapture installation directory (e.g., `C:\Users\YourUser\FireCapture_v2.7.15`).
2. Go to the 64-bit plugins directory: `plugins\x64\`.
3. Create a dedicated folder named `AutofocusPlugin`.
4. Place the compiled plugin file (`AutofocusPlugin.jar`) inside this folder: 
   `FireCapture_v2.7.15\plugins\x64\AutofocusPlugin\AutofocusPlugin.jar`

---

## **2. Focuser Connection & Troubleshooting**

* Ensure that your focuser is properly connected and communicating via **ASCOM**, **CPWI**, or your preferred hardware control software before starting FireCapture.
* **Troubleshooting Note:** If FireCapture fails to detect focuser movements or commands during setup, temporarily toggle the FireCapture focuser connection option *Off* and back *On* to force a complete reset of the ASCOM communication bridge.

---

## **3. Enabling the Plugin in FireCapture**

1. Launch FireCapture and connect your camera.
2. Locate the **Pre-processing** panel on the left side of the interface.
3. Click on the filter/plugin dropdown menu (initially set to "None").
4. Select **"Lunar/Planetary Autofocus"** from the list to enable the live overlay panel.

---

## **4. Core Prerequisites**

* **Initial Focus:** The target (Moon, Sun, or Planet) must already be close to optimal focus (rough manual focus or achieved via Bahtinov / Tri-Bahtinov mask). If the image is completely out of focus (large doughnut shapes), contrast gradients will be insufficient to trace a proper V-Curve.
* **Auto-Alignment Recommendation:** It is strongly recommended to enable FireCapture's built-in **"Auto-alignment"** option (located in the left options panel) during your session. This ensures the target stays perfectly centered inside your Sub-ROI while the focuser moves through its steps.

---

## **5. Calculation Modes (Moon/Sun vs Planets)**

1. **LUNA / SUN Mode (Pure Gradient Analysis):**
   - *How it works:* Computes absolute spatial gradients ($dx, dy$) pixel by pixel across the frame or active Sub-ROI.
   - *Why use it:* Lunar and solar surfaces feature high-contrast details (craters, sunspots, filaments). Pure gradients sharply reward crisp edges, generating a steep and reliable V-Curve.

2. **PLANET Mode (Intensity-Weighted Analysis):**
   - *How it works:* Uses a hybrid formula combining squared gradients with normalized average brightness.
   - *Why use it:* Planets (Jupiter, Saturn, Mars) are bright disks surrounded by black space. Pure gradients would be skewed by background noise or atmospheric seeing spikes. Intensity weighting isolates fine cloud details and ring structures safely.

---

## **6. Advanced Features & Testing**

- **Anchored Sub-ROI:** Click "Select Area" to draw a rectangle around a specific feature (e.g., a crater or planet). Processing only this area speeds up calculations and blocks out background sky noise.
- **Lucky Autofocus & Settle Time:** During the focuser stabilization pause (configurable from 500ms to 3000ms), the plugin multi-samples frames in streaming, picking the sharpest frame where seeing momentarily stabilized.
- **"Difficult Seeing" Mode (Smart Stacking & Robust Fit - V2.8):** Ideal for turbulent nights. It applies local Smart Stacking (discarding the worst 50% of frames and taking the median of the best half per step) combined with a robust parabolic fit to eliminate false peaks caused by seeing oscillations.
- **Temporal Throttling:** Adjust sampling frequency (every frame, 250ms, 500ms, or 1s) to keep FireCapture's live preview fluid.
- **Parabolic Interpolation & Surgical Positioning:** Calculates the ideal parabola ($y = ax^2 + bx + c$), finds the precise sub-step vertex ($X_v = -b/2a$), and commands the final backlash-corrected move.
- **Dummy Cam Testing:** Fully supports offline simulation using FireCapture's virtual *DummyCam*, allowing you to test V-Curve behavior without hardware.
- **12-Language Multilingual Support:** Instantly switch languages from the top-right menu with real-time UI synchronization (English, Italian, French, German, Spanish, Chinese, Japanese, Korean, Russian, Polish, Portuguese, and Dutch).
---

## **7. Automatic CSV Data Logging**

- **V-Curve Data Export:** Upon completing a successful autofocus routine (both in DummyCam test mode and live sessions), the plugin automatically generates and saves a **CSV file** containing all calculated V-Curve coordinates and metrics.
- **Save Directory (`user.home`):** Saved directly in your system's user home directory for easy access:
  - **Windows:** `C:\Users\<YourUsername>\`
  - **Linux / macOS:** `/home/<YourUsername>/` (or user root directory)

*Clear skies and perfect focus!*
![Interfaccia del Plugin](./screenshot%20app.jpg)
