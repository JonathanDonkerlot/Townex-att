# Townex Watch

A native client-side MelonLoader VR wrist-screen mod for *A Township Tale* (PCVR, Mono).
**Townex Watch** projects a clean, screen-only `WorldSpace` UI floating directly above the back of the **local player's** hand—with zero 3D housing meshes, zero hand clipping, double-sided materials so it stays visible from every viewing angle, and zero external AssetBundle dependencies.

---

## Features & Watch Faces

* **Screen-Only Back-of-Hand Mount:** Computes the dorsal hand plane directly from ATT's `wrist_{L|R}_jnt` and finger root joints (`indexRoot`, `middleRoot`, `littleRoot`) so the screen floats cleanly above the back of the hand facing upwards, without clipping inside the mesh.
* **Always-Visible Double-Sided UI (Optional Gaze Sleep):** Uses double-sided UI/font materials (`Cull Off`) and offset depth layers so it never disappears or Z-fights at oblique angles. `EnableGazeWake` is off by default (can be enabled in config if you want tilt/swing auto-sleep).
* **Tactile VR Finger-Tap Interaction:** Tap anywhere on the screen with your opposite index fingertip (`0.35s` debounce cooldown) with spatial audio click + XR controller haptic feedback.
* **Three Diegetic Watch Faces:**
  1. **Vitals & Perf:** Smoothed VR FPS & frame time (`ms`), live Health / Hunger / Stamina percentages, local system clock, and session timer.
  2. **Cartographer & World Clock:** Live `(X, Y, Z)` world position, cave depth / surface elevation, 8-sector compass heading (`N`–`NW` + degrees), in-game `HH:MM` time, and exact Dawn/Dusk countdown.
  3. **Gear Inspector:** Displays remaining durability percentage (`DurabilityModule.Integrity`) for held tools/weapons and belt/back holstered items.

---

## In-Game Controls

### VR Controls
* **Cycle Screen Face:** Tap the screen with your opposite index fingertip.

### Desktop Diagnostic Hotkeys (Configurable)
* **`F8`** — Prints a full runtime diagnostic report to the MelonLoader log/console (resolved wrist/fingertip bones, computed back-of-hand mount basis, active `StatManager` stat names, `GameTimeManager` state, and equipped gear).
* **`F9`** — Cycles the active screen face.

---

## Configuration (`UserData/MelonPreferences.cfg`, `[TownexWatch]`)

Editing `UserData/MelonPreferences.cfg` live triggers MelonLoader's preference reload and automatically re-mounts the screen with the new settings.

| Key | Default | Description |
|---|---|---|
| `DominantWrist` | `"Left"` | Hand to mount the screen (`"Left"` or `"Right"`). Tap fingertip uses the opposite hand. |
| `EnableGazeWake` | `false` | When `false`, stays visible from all angles; when `true`, sleeps when tilted away or swung. |
| `WakeAngleDegrees` | `85` | Gaze angle threshold (degrees) between screen normal and eye vector when `EnableGazeWake` is `true`. |
| `WakeHysteresisDegrees` | `10` | Extra angle beyond `WakeAngleDegrees` before sleeping again. |
| `SwingSpeedThreshold` | `2.2` | Hand speed (m/s) that forces sleep when `EnableGazeWake` is `true`. |
| `SwingHoldoffSeconds` | `0.6` | Seconds the screen stays asleep after a fast swing ends. |
| `FadeSpeed` | `6.0` | Display alpha fade speed (1/sec) when `EnableGazeWake` is `true`. |
| `WatchScale` | `1.0` | Uniform scale of the screen (`0.4`–`3.0`). |
| `BackOfHandLiftMeters` | `0.038` | Lift distance (meters) above the back-of-hand bone plane. |
| `LocalPosOffsetX/Y/Z` | `0, 0, 0` | Extra local position offset (meters) in screen space. |
| `LocalRotOffsetX/Y/Z` | `0, 0, 0` | Extra local Euler rotation (degrees) in screen space. |
| `EnableFaceVitals` | `true` | Include Face 1 (Vitals & Performance) in cycle order. |
| `EnableFaceCartographer` | `true` | Include Face 2 (Cartographer & World Clock) in cycle order. |
| `EnableFaceGear` | `true` | Include Face 3 (Tool & Gear Inspector) in cycle order. |
| `NorthOffsetDegrees` | `0` | Compass rotation offset (degrees) added to Unity `+Z` North. |
| `ClockOffsetHours` | `6` | Hour corresponding to `GameTimeManager` normalized dawn (`0.0`). |
| `SurfaceReferenceY` | `128` | Baseline Y coordinate (meters) for Cave Depth vs Elevation display. |
| `TapCooldownSeconds` | `0.35` | Global debounce cooldown (seconds) between taps. |
| `HapticStrength` | `0.45` | XR controller haptic impulse amplitude (`0.0`–`1.0`). |
| `AttachInMainMenu` | `false` | Attach on main menu rigs as well as gameplay `PlayerCharacter`. |
| `EnableDiagnosticHotkeys` | `true` | Enable `F8` / `F9` keyboard shortcuts. |
