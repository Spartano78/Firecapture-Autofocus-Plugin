# 🔭 Lunar / Solar / Planetary Autofocus Plugin for FireCapture (V2.9.9)
---
[![GitHub All Downloads](https://img.shields.io/github/downloads/Spartano78/Firecapture-Autofocus-Plugin/total.svg)](https://github.com/Spartano78/Firecapture-Autofocus-Plugin/releases)

Professional autofocus plugin for FireCapture, developed by Stefano Romani, designed specifically for high-resolution planetary, lunar, and solar imaging with motorized focusers across all platforms (Windows/ASCOM and Linux/INDI).

[![YouTube](https://img.youtube.com/vi/DVSCTCL4s40&t=151s/hqdefault.jpg)](https://www.youtube.com/watch?v=DVSCTCL4s40&t=151s)

## 📜 Version History (v2.9.9 to v2.9.2) 

### See full changelog in download sections for the detailed improvements in each version and *please* read the Omnibus Multilanguage Manual (12 languages, less than 5 minutes reading) before starting using the plugin!

### [2.9.9] - 2026-10-15

- **Universal Absolute & Relative Focuser Compatibility (Cross-Platform Engine):** Re-engineered moveFocuser() with dynamic runtime driver reflection. Automatically queries the connected focuser's operational mode (isAbsolute()) and current hardware position (getPosition()). When an absolute controller is detected (such as ZWO EAF under Linux/INDI, Rigel USB-nStep, MoonLite, Feather Touch, or Esatto), relative step commands are seamlessly translated into absolute target coordinates (targetPos = currentPos + steps). Completely eliminates motor stalling, drawtube freezing, and accidental defocusing caused by absolute drivers ignoring relative offsets.

- **Seamless Relative Focuser Fallback:** Retains native relative stepping (moveBy() / move()) for traditional open-loop DC focusers and relative stepper controllers lacking positional encoders, guaranteeing 100% universal hardware compatibility across Windows (ASCOM) and Linux (INDI) without requiring any manual UI toggles or user intervention.

- **Dense 1x1 Sub-ROI Gradient Sampling (Moon & Sun Mode):** Optimized the spatial gradient calculation engine in FocusCalculator for both monochrome (8-bit) and OSC debayered color streams. When an anchored Sub-ROI is selected around lunar craters, rilles, sunspots, or solar granulation, the calculation loop dynamically switches from 2x2 decimation to full-resolution 1x1 pixel sampling (step = 1). Evaluating 100% of the pixels yields maximum edge sensitivity and an ultra-sharp, unambiguous focus peak.

- **Full-Frame Performance Protection:** Automatically preserves the high-speed 2x2 pixel stride (step = 2) when scanning full-frame sensors without Sub-ROI, keeping live video frame rates 100% fluid and latency-free.

### [2.9.8] - 2026-10-12

- **Dual-Mode Interface Selector (Expert Mode):** Added a dedicated [ ] Expert Mode checkbox inside the Step Size configuration panel. In Standard Mode (default), the interface remains streamlined with standard dropdown presets (5, 10, 15, 20) and a safe 50-step backlash; checking Expert Mode dynamically reveals direct numeric input fields initialized to 0 for full manual configuration.

- **Fully Customizable Step Size Field:** Replaced fixed dropdown constraints in Expert Mode with an open numeric input field, allowing astrophotographers to define custom motor increments of any size (e.g., 30, 50, 100, 200+ steps). This enables optimal sampling for ultra-high-resolution motorized focusers (such as ZWO EAF with 5,760 steps/rev, Feather Touch, MoonLite, and Optec) with an automated safety fallback to 20 steps if an invalid or zero value is entered.

- **User-Configurable Backlash Compensation:** Introduced a dedicated manual Backlash input field in Expert Mode, allowing users to override the hardcoded 50-step margin and set custom gear play values (0 to 500+ steps). Designed specifically for Schmidt-Cassegrain (SCT) primary mirror shift, 1:10 belt-drive reductions, or heavily geared motors. Custom backlash margins are dynamically applied both during initial sweep prep and final vertex return.

- **Hardware Safety Warning & Dedicated Tooltips:** Implemented informative, auto-hiding tooltips on both custom fields. The Backlash tooltip features a prominent, bold MECHANICAL DAMAGE WARNING alerting users to the risk of motor strain, belt stripping, or focuser jamming if excessive values exceeding the focuser's physical drawtube travel are entered.

- **Parabolic Fit Quality Metric (R² Coefficient of Determination):** Integrated mathematical evaluation via AutoFocusMath.calculateR2(...) to calculate the formal coefficient of determination between live Lucky AF sharpness samples and the theoretical regression parabola $y = ax^2 + bx + c$.

- **Tri-Color Real-Time Vertex Diagnostics & False-Peak Abort:** The V-Curve chart monitor dynamically displays the live $R^2$ score and updates the vertex color: Emerald Green ($R^2 \ge 0.85$) for robust, mathematically certain focus; Amber/Orange ($0.65 \le R^2 < 0.85$) for acceptable yet noisy seeing; and Red ($R^2 < 0.65$) for unreliable scans. If $R^2 < 0.65$, motor repositioning is automatically aborted to prevent false focus caused by wind gusts or clouds, prompting an alert dialog to repeat the scan.

- **Instant 12-Language Synchronization:** All new labels, toggle states, tooltips, mechanical safety warnings, and fit quality alerts are fully localized across all 12 supported languages with seamless runtime switching and native font rendering.

### [2.9.7] - 2026-10-12

- **Dedicated Saturn Mode:** Added a specialized third optical target mode ("Saturn") alongside "Moon/Sun" and "Planets", specifically engineered for ringed planetary systems to maximize sharpness contrast while discarding background sky noise.

- **Interactive WinJUPOS-Style Vector Wireframe:** Implemented an on-screen wireframe mask modeled after WinJUPOS planetary measurements (featuring the central globe, Ring A, Ring B/Cassini division, and polar axis with N/S orientation marks). Supports full interactive control: click/drag to position, mouse wheel to scale, and Shift + Wheel (or Left/Right arrow keys) to adjust ring inclination angle.

- **Out-of-Focus Expansion Tolerance Envelope (+25% Padding):** Integrated a smart elliptical safety envelope with 25% extra tolerance surrounding the globe and rings. This prevents planet "bloating" and light spillover from clipping outside the calculation area during deep out-of-focus V-Curve sampling points.

- **High-Visibility Transparent Overlay:** Upgraded the selection overlay to 100% full background transparency and an ultra-subtle tint (alpha 10 / 96% transparent) over the target, ensuring optimal planetary contrast and visibility on the live camera stream beneath the mask.

- **Dynamic HUD Localized Fonts (CJK & Korean Fix):** Enhanced the on-screen display HUD to dynamically resolve localized system fonts (including Malgun Gothic for Korean Hangul and East Asian font families), eliminating character clipping and rendering issues across all 12 supported languages.

- **Sensor Noise Gate & High-Gain Floor Rejection:** Implemented a hardware-level gradient threshold (gradSq > 8) in both Planets and Saturn calculation engines to discard CMOS sensor readout and thermal noise at high gain settings. Eliminates artificial background sky elevation, producing a significantly steeper, cleaner, and more pronounced V-Curve vertex.

- **Dynamic Planetary Luminance Normalization:** Re-engineered the brightness weighting algorithm to compute average intensity strictly across valid planetary disk pixels (ignoring dark sky values < 12 ADU) and normalized the sharpness score by division. This ensures complete immunity against passing atmospheric haze, cloud transparency drops, or crepuscular background sky darkening.

- **Runtime Settle Time Synchronization:** Fixed dynamic synchronization for the stabilization delay dropdown (500 ms to 3000 ms), ensuring user-selected focuser settle pauses are directly read and fully honored at routine launch before sharpness frame collection starts.

- **Mechanical Settling Pause (150 ms):** Added a dedicated 150 ms post-step delay prior to frame acquisition, allowing the motor and mechanical drawtube to come to a complete physical halt and dissipating micro-vibrations before taking Lucky AF measurements.

- **Bidirectional Return Anti-Backlash:** Implemented proactive backlash overshoot and return compensation (+50 steps forward engage) when reversing direction to lock onto the calculated parabolic vertex at the end of the scan. This eliminates focuser gear deadband and ensures the drawtube physically moves to the optimal focus position instead of slipping.

- **Completion Dialog Vertex Step Fix:** Resolved a UI reporting bug in JOptionPane where the raw peak sharpness score was displayed instead of the calculated physical motor step position (optimalOffset), providing accurate numerical feedback on the final focuser position.

### [2.9.6] - 2026-10-08

- **Automatic Language Detection & Fallback:** Implemented auto-detection at plugin startup by checking both the operating system language and FireCapture settings, with a secure fallback to English (EN) if the language is missing or unrecognized.

- **Comprehensive Interactive Tooltips:** Added dynamic, auto-hiding tooltips across all plugin functions, panels, and menus, providing instant descriptive guides and explanations for every control.

### [2.9.5] - 2026-10-07

- **Unblocked Video/Photo Recording (capture() Fix):** Fixed a critical issue where FireCapture failed to start or write video recordings (SER/AVI) and snapshots while the plugin was enabled, by ensuring capture() returns true to authorize capture stream execution.

- **Full Color Camera Support (computeColor Implementation):** Implemented high-speed color sharpness calculation in computeColor() using fast RGB-to-luminance weighting, ensuring full compatibility for OSC color cameras (such as the Uranus-C) in debayered modes.

- **Null Filter Buffer Bypass (isNullFilter()):** Configured isNullFilter() to return true, signaling to FireCapture that the plugin does not alter image buffer memory. This allows FireCapture to bypass extra memory allocations and stream frames directly to the disk recorder.

- **Zero-Latency Capture Pass-Through:** Engineered an instant 0ms pass-through mechanism in both computeMono and computeColor during active recording (isCapturing == true), preserving 100% CPU and USB bandwidth for maximum frame rates.

### [2.9.2] - 2026-10-06

- **Real-Time V-Curve Chart Panel:** Added a dedicated side-panel featuring a live, anti-aliased V-Curve graph with a light gray background, grid system, and parabolic fitting curve ($y = ax^2 + bx + c$) rendered in crimson red.

- **Optimal Vertex & Axis Labels:** Integrated dynamic emerald-green vertex indicators and fully localized axis labels for both the X-axis (Focuser Position) and Y-axis (Sharpness Score).

- **UI Layout Stability & Multilingual Support:** Fixed the upper toolbar layout so it remains securely anchored when opening/closing the side chart panel, and implemented robust dynamic font rendering for complete character support across all 12 supported languages.

- **Capture Blocking Bug Fix:** Resolved an issue where FireCapture was prevented from capturing photos or recording videos while the plugin interface remained open, by correctly integrating event flags (captureStarted() / captureStoped()).


## 🚀 Installation

1. Navigate to your main FireCapture installation directory (e.g., C:\Users\YourUser\FireCapture_v2.7.15).
2. Go to the 64-bit plugins directory: plugins\x64\.
3. Create a dedicated folder named AutofocusPlugin.
4. Place the compiled plugin file (AutofocusPlugin.jar) inside: FireCapture_v2.7.15\plugins\x64\AutofocusPlugin\AutofocusPlugin.jar.


## 🌐 Multilingual User Guide

For detailed instructions, troubleshooting notes, and tips in all 12 supported languages, check the **"Manual_Omnibus_12_Languages_Firecapture_Autofocus-v2.9.9.pdf"** in the releases section.


## ☕ Support the Developer

If this plugin helps you capture stunning celestial details, consider supporting the project.
[![PayPal Me](https://img.shields.io/badge/PayPal.Me-Donate-orange?style=flat&logo=paypal)](https://paypal.me/stefanoromani195)


*Developed with passion by Stefano Romani*
