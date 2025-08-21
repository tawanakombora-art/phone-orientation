# 📱 Phone Upside-Down Detector

A simple **HTML + CSS + JavaScript** page that detects when a smartphone is held upside-down and shows the result in the center of the screen.

It uses the browser’s **Screen Orientation API** when available, and falls back to the **accelerometer (DeviceMotion API)** when needed. Works best over **HTTPS** on real mobile devices.

---

## 🚀 Demo

When you open the page on your phone:

- If the device is upright → **Normal** (green).
- If the device is rotated 180° (upside down) → **Upside Down** (red).
- You’ll also see supporting debug info: orientation type, angle, and accelerometer readings (X, Y, Z).

---

## ⚙️ How It Works

1. **Screen Orientation API**
   - Most modern browsers expose `screen.orientation.type` and `screen.orientation.angle`.
   - When the type is `portrait-secondary` or the angle is 180°, the phone is upside down.

2. **DeviceMotion Fallback**
   - If orientation data is missing or rotation lock is enabled, the script listens to `devicemotion` events.
   - It checks the **Y-axis** gravity reading from the accelerometer:
     - Positive Y ≈ upright.
     - Negative Y ≈ upside down.
   - A tolerance (`T = 4.0`) avoids false triggers when tilted diagonally.

3. **iOS Permission Handling**
   - Since iOS 13+, motion sensors require explicit user permission.
   - If the browser blocks access, a **“Enable motion access”** button is shown. Tapping it requests permission with `DeviceMotionEvent.requestPermission()`.

---

## 📂 Project Structure

- `index.html` → Main file with HTML, CSS, and JS all in one.
  - **UI**: a centered card with status text and debug info.
  - **Style**: dark background with bright feedback colors.
  - **Script**: initializes listeners, requests iOS permission if needed, updates the UI in real-time.

---

## ✅ Requirements

- A modern **mobile browser** (Chrome, Safari, Firefox, Edge).
- Page should be served over **HTTPS** (some motion APIs are blocked on `http://`).
- Test on an actual phone (desktop emulators don’t expose accelerometer data).

---

## 🔧 Customization

- **Tolerance**: Adjust `const T = 4.0` in the script for sensitivity.
- **UI**: Change colors in the CSS variables at the top (`--ok`, `--bad`, etc.).
- **Output**: Use the `render(payload)` function if you want to log or trigger other actions when orientation changes.

---

## 📜 License

MIT – free to use and adapt.
