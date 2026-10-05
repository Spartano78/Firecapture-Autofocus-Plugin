# 🔭 Lunar / Solar / Planetary Autofocus Plugin for FireCapture (V2.9)

[![GitHub All Downloads](https://img.shields.io/github/downloads/Spartano78/Firecapture-Autofocus-Plugin/total.svg)](https://github.com/Spartano78/Firecapture-Autofocus-Plugin/releases)

Professional autofocus plugin for **FireCapture**, developed by **Stefano Romani**, designed specifically for high-resolution planetary, lunar, and solar imaging with motorized focusers (e.g., Celestron via ASCOM/CPWI).

---
> ⚠️ **IMPORTANT NOTICE (Known Bug):**
> If the plugin remains active in the menu when starting a video or image capture, FireCapture's interface shows the recording timer running, but no actual frames are saved to disk. 
> * **Workaround:** Explicitly disable the plugin from the menu before starting any capture.
> * **Status:** A fix is currently being developed and will be released in an upcoming update.
---
## ✨ Key Features (V2.9)

* **Dual Dropdown Step Configuration & Backlash Management:** Intuitive dropdown menus for **Step Size** (5, 10, 15, 20) and **Steps Count** (10, 15, 20) to control the scanning range. Paired with precise mechanical backlash recovery (reversing by scan radius + a reduced safety margin of 50 steps, then advancing by margin) for a perfectly symmetrical V-Curve while preventing tracking loss.
* **Real-time Scan Progress Counter:** Live status display showing `Step X/20` (matching the selected total steps) during the scanning process, fully localized across all supported languages.
* **GitHub Update Checker:** Automated online version checking directly from the GUI with secure TLS protocol handling to notify users of new releases.
* **Advanced V-Curve Engine:** Least squares parabola calculation ($y = ax^2 + bx + c$) for high-precision focus vertex detection ($X_v = -b/2a$).
* **Dual Calculation Mode:**
  * **Moon/Sun Mode:** Absolute spatial gradient analysis ($dx, dy$) pixel by pixel for high-contrast lunar craters and solar features (H-alpha / white light).
  * **Planet Mode:** Hybrid weighted analysis with normalized average intensity to isolate planetary details while reducing seeing impact.
* **Anchored Sub-ROI (Software):** Isolate a specific target box to optimize processing speed and eliminate background noise.
* **Lucky Autofocus & Settle Time:** Multi-frame capture during stabilization pauses (selectable from 500ms to 3000ms) to automatically select the sharpest frame where seeing momentarily stabilized.
* **"Difficult Seeing" Mode:** Smart Stacking and Robust Parabolic Fit to stabilize sharpness analysis under turbulent atmospheric conditions.
* **Automatic CSV Data Logging:** Automatically exports V-Curve coordinates and metrics to a `.csv` file in your system's user home directory (`user.home`).
* **Temporal Throttling & Dummy Cam Support:** Frame sampling control to keep FireCapture's video stream 100% fluid, fully operational even with offline virtual cameras.
* **12-Language Support:** Instant switching with real-time UI synchronization for Italian, English, Spanish, French, German, Portuguese, Polish, Dutch, Simplified Chinese, Traditional Chinese, Japanese, and Korean.

---

## 🚀 Installation

1. Navigate to your main FireCapture installation directory (e.g., `C:\Users\YourUser\FireCapture_v2.7.15`).
2. Go to the 64-bit plugins directory: `plugins\x64\`.
3. Create a dedicated folder named `AutofocusPlugin`.
4. Place the compiled plugin file (`AutofocusPlugin.jar`) inside: `FireCapture_v2.7.15\plugins\x64\AutofocusPlugin\AutofocusPlugin.jar`.

---

## 🌐 Multilingual User Guide

For detailed instructions, troubleshooting notes, and tips in all 12 supported languages, check the Multilingual User Guide in download section.

---

## ☕ Support the Developer

If this plugin helps you capture stunning celestial details, consider buying me a coffee:
[![PayPal Me](https://img.shields.io/badge/PayPal.Me-Donate-orange?style=flat&logo=paypal)](https://paypal.me/stefanoromani195)

---
*Developed with passion by Stefano Romani.*
