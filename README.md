# 🌟 Neon Aura AR — Hand & Face Tracking Experience

> A browser-based Augmented Reality experience powered by **MediaPipe AI** — no installs, no plugins, just your webcam and imagination.

---

## 📸 Overview

**Neon Aura AR** is a real-time, AI-powered web application that uses your webcam to:
- Track **both hands** and overlay stunning neon visual effects
- Detect your **face** and render a dynamic cyber-mask
- Let you **play gesture-controlled games** — all in the browser

Everything runs locally using vanilla HTML, CSS, and JavaScript — zero backend required.

---

## ✨ Features

### 🖐 Hand Tracking AR (`index.html`)
| Feature | Description |
|---|---|
| **Matrix Rain Background** | Katakana characters that speed up when you move your hands fast |
| **Neon Skeleton** | Glowing hand skeleton drawn over your webcam feed |
| **Fingertip Sparks** | Constant particle sparks emitted from each fingertip |
| **Cross-Hand Lightning** | Electric arcs jump between fingers of both hands when close |
| **Rainbow Connecting Lines** | Animated gradient lines drawn between both hands |
| **Rotating Mandala** | Geometric star pattern drawn when all 10 fingers are visible |
| **Pinch Gesture** | Creates a neon shockwave ripple + triggers a "zap" sound |
| **Gesture Detection** | Detects Open Hand, Fist, and Pinch in real-time |
| **5 Color Themes** | Rainbow, Cyberpunk, Lava, Ocean, Galaxy — switchable live |
| **Web Audio Engine** | Ambient hum that changes pitch/volume based on hand distance |

### 👁 Face Detection (`index.html` — toggleable)
| Feature | Description |
|---|---|
| **Face Mesh Wireframe** | Subtle 468-point tesselation over your face |
| **Neon Contours** | Bright glowing outlines of eyes, eyebrows, lips, face shape |
| **Iris Glow** | Cyborg-style glowing rings tracking your pupils |
| **Mouth Energy Burst** | Radial glow emits from your mouth when you open it |
| **Toggle On/Off** | Enable/disable independently — saves CPU when not needed |

### 🎮 Hand Gesture Games (`games.html`)
#### 🏎️ Neon Car Racer
- Race on a **5-lane neon highway** against **4 AI competitor cars**
- Cars change lanes, race at different speeds, and block your path
- Tilt your hand **left/right** to steer
- Raise **☝️ index finger** for a speed boost
- Live **leaderboard** and animated **speedometer**

#### 🏃 City Marathon Run
- **5 runners** race together — you + 4 AI NPCs with unique looks
- Each NPC is a fully animated **human stick figure** with head, hair, torso, arms, legs
- NPCs **auto-jump** over obstacles and get **eliminated** if they hit one
- **☝️ Index Up** = Jump | **✊ Fist** = Duck
- Collect coins, dodge ground spikes and laser beams
- Live **race status panel** showing which runners are still going

---

## 🕹️ Controls Reference

### AR Page (`index.html`)
| Gesture | Effect |
|---|---|
| ✋ **Move hand fast** | Matrix rain accelerates |
| 👌 **Pinch** (thumb + index) | Shockwave + Zap sound |
| 🖐 **Open Hand** | Full fingertip sparks |
| ✊ **Fist** | Detected in HUD |
| 🤲 **Both hands close** | Electrical arcs between fingertips |
| 🙌 **All 10 fingers** | Rotating mandala effect |

### Car Racer (`games.html`)
| Gesture | Effect |
|---|---|
| 🖐 **Tilt hand left** | Steer car left |
| 🖐 **Tilt hand right** | Steer car right |
| ☝️ **Index finger up** | Activate BOOST |

### City Marathon Run (`games.html`)
| Gesture | Effect |
|---|---|
| ☝️ **Index finger up** | Jump over obstacles |
| ✊ **Fist** | Duck under laser beams |

---

## 🗂️ Project Structure

```
connect/
│
├── index.html        # Main AR experience (hand + face tracking, themes, audio)
├── games.html        # Hand gesture games hub (car racer + endless runner)
└── README.md         # This file
```

---

## 🚀 How to Run

### Option 1 — Direct in Browser
Just open `index.html` in any modern browser (Chrome recommended).

> ⚠️ **Note:** Your browser will ask for **camera permission** — this is required for hand/face tracking. No video is stored or transmitted anywhere.

### Option 2 — Local Development Server (Recommended)
Some browsers block camera access for `file://` URLs. Use a simple local server:

```bash
# Python 3
python -m http.server 8080

# Node.js (npx)
npx serve .

# VS Code — install "Live Server" extension and click "Go Live"
```

Then open: `http://localhost:8080`

### Browser Compatibility
| Browser | Status |
|---|---|
| ✅ Google Chrome | Fully supported (recommended) |
| ✅ Microsoft Edge | Fully supported |
| ⚠️ Firefox | Partial (WebGL may differ) |
| ❌ Safari | Limited (WebRTC constraints) |

---

## 🛠 Tech Stack

| Technology | Purpose |
|---|---|
| **HTML5 Canvas** | All AR rendering (dual-canvas pipeline) |
| **Vanilla JavaScript** | Game logic, physics engine, gesture detection |
| **CSS3** | Glassmorphism UI, animations, themes |
| **[MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker)** | Real-time 21-point hand landmark detection |
| **[MediaPipe Face Mesh](https://developers.google.com/mediapipe/solutions/vision/face_landmarker)** | Real-time 468-point face landmark detection |
| **Web Audio API** | Procedural sound synthesis (hum + zap effects) |
| **WebRTC / Camera API** | Webcam access |

---

## ⚙️ Architecture Notes

### Dual Canvas Pipeline
The app uses **two stacked canvases** for performance:
- `bgCanvas` — renders the matrix rain background with trailing fade effect
- `mainCanvas` — renders hand/face overlays using `globalCompositeOperation: 'screen'` for neon bloom

### Lazy Face Mesh Loading
Face detection is **off by default**. The `FaceMesh` WASM model is only downloaded and initialized the first time you click **"👁 Face: ON"** — keeping startup fast and saving CPU for users who don't need it.

### MediaPipe Integration
A single `Camera` instance feeds video frames to both AI models. Each model runs its own inference pipeline asynchronously:
```
Camera frame → Hands model  → currentHands[] → render loop
            → FaceMesh model (if ON) → currentFaces[] → render loop
```

---

## 🎨 Themes

Switch themes using the bottom navigation bar:

| Theme | Colors |
|---|---|
| **Rainbow** | Full HSL spectrum cycling over time |
| **Cyberpunk** | Alternating Red `#ff003c` and Cyan `#00f0ff` |
| **Lava** | Warm oranges and deep reds, intensity pulses with time |
| **Ocean** | Cool blues and teals |
| **Galaxy** | Deep purples and violets, slow sine wave shift |

---

## 📄 License

This project is open source and free to use for educational and personal projects.

---

## 👨‍💻 Author

<table>
  <tr>
    <td align="center">
      <strong>Updesh Singh</strong><br/>
      B.Tech — Computer Science & Engineering<br/>
      Specialization: <strong>Artificial Intelligence & Machine Learning (AIML)</strong><br/>
      🏛️ <strong>GLA University</strong>, Mathura, India
    </td>
  </tr>
</table>

---

## 🙏 Credits

- **[MediaPipe](https://mediapipe.dev/)** by Google — AI hand & face tracking
- **[Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)** — Browser-native sound synthesis
- **[Google Fonts — Orbitron & Inter](https://fonts.google.com/)** — Typography

---

*Built with ❤️ by **Updesh Singh** · B.Tech CS (AIML) · GLA University*
