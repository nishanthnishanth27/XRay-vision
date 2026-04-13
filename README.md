<p align="center">
  <img src="https://img.shields.io/badge/Engine-X--Ray_Portal_v5-00ffcc?style=for-the-badge&labelColor=000000" />
  <img src="https://img.shields.io/badge/Particles-10,000-0088ff?style=for-the-badge&labelColor=000000" />
  <img src="https://img.shields.io/badge/Powered_By-MediaPipe_Holistic-ff4488?style=for-the-badge&labelColor=000000" />
  <img src="https://img.shields.io/badge/Zero_Dependencies-Vanilla_JS-ffcc00?style=for-the-badge&labelColor=000000" />
</p>

<h1 align="center">
  ☢️ X-Ray Hand Portal Engine
</h1>

<p align="center">
  <strong>A real-time AR X-Ray scanner that turns your webcam into a sci-fi medical imaging portal.</strong><br/>
  Use both hands to open a portal window and reveal a glowing, particle-based neural body scan — complete with anatomical zones, skeletal overlays, heartbeat monitors, and live telemetry HUD.
</p>

<p align="center">
  <code>HTML</code> · <code>Canvas 2D</code> · <code>MediaPipe Holistic</code> · <code>No Build Step</code>
</p>

---

## 🎬 How It Works

1. **Show both hands** to the webcam
2. **Pinch your index fingers and thumbs close together** (~150px) to activate the portal
3. **Spread your hands apart** to expand the X-Ray scanning window
4. Watch as **10,000 square particles** form a dense, anatomically-colored body silhouette inside the portal

The portal is clipped to the quadrilateral formed by your four finger landmarks — it moves, scales, and rotates with your hands in real-time.

---

## ✨ Features

### 🧬 Neural Particle Body System
- **10,000 square particles** distributed across the body using MediaPipe's segmentation mask
- **Anatomical color zones** — head (white/cyan), chest (pink), arms (teal), hands (gold), core (purple), legs (blue), feet (orange)
- **3-layer depth rendering** — BACK, MID, FRONT layers with progressive opacity and size scaling
- **Energy surge waves** — periodic radial pulses that ripple outward from the chest center

### 🦴 Body Detection & Tracking
- **MediaPipe Holistic** for simultaneous hand + pose + segmentation tracking
- **Mask-based particle redistribution** — particles fill the actual body silhouette, not a generic shape
- **Head dome generator** — 1,500 dedicated particles form a dense cranial coverage zone
- **Body path clipping** — all particles are constrained within an anatomically-accurate polygon

### 🖥️ Sci-Fi HUD System
- **Live data panel** — floating HUD near the shoulder with bioscan telemetry
- **Rotating radar** — animated crosshair/radar indicator
- **Joint telemetry tags** — micro-labels on elbows and knees showing real-time confidence percentages
- **Pipeline status bar** — INPUT → DETECT → POSE → PORTAL → COMP → OUTPUT node chain
- **Frame counter** with glitch error indicators

### ⚡ Portal Effects
- **Spark bursts** — particle explosions when fingers first connect
- **Topographic ripple echoes** — expanding contour waves around the body outline
- **Human head/neck silhouette generator** — cranium dome, jaw, ears, and neck trapezius mapped from ear/nose landmarks
- **3D perspective grid** — vanishing-point grid that tracks head position
- **Dual-layer scan grid** — fine (8px) and coarse (40px) cyan grid overlay
- **Laser scanline** — sweeping horizontal scan beam with gradient trail
- **Data stream columns** — rising vertical data packets within the body path

### 🔥 Glitch System
- **Random scan interrupts** — periodic glitch events with:
  - Horizontal slice displacement
  - White noise flash
  - Corrupt hex text overlays (`0xFFE3 >> CORRUPT`, `ERR: SEG FAULT`)
  - Red "SCAN INTERRUPT" warning
- **Digital jitter** — particles scatter during glitch frames

### 🎯 Portal Mechanics
- **Temporal smoothing** — portal window position lerps for silky-smooth tracking
- **Body drift compensation** — all 10K particles shift with chest movement delta
- **Animated corner markers** — glowing turquoise squares at each portal vertex
- **Chromatic border** — animated hue-shifting portal frame with glow

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────┐
│                   BROWSER (Single HTML)              │
├─────────────────────────────────────────────────────┤
│                                                      │
│   ┌──────────┐    ┌──────────────┐    ┌──────────┐  │
│   │  WebCam   │───▶│  MediaPipe   │───▶│  Canvas  │  │
│   │  Stream   │    │  Holistic    │    │  2D Ctx  │  │
│   └──────────┘    └──────┬───────┘    └────┬─────┘  │
│                          │                  │        │
│              ┌───────────┼──────────────────┘        │
│              │           │                           │
│   ┌──────────▼──┐  ┌─────▼─────┐  ┌──────────────┐  │
│   │  Hand       │  │  Pose     │  │ Segmentation │  │
│   │  Landmarks  │  │  Landmarks│  │ Mask         │  │
│   │  (2 hands)  │  │  (33 pts) │  │ (body fill)  │  │
│   └──────┬──────┘  └─────┬─────┘  └──────┬───────┘  │
│          │               │               │           │
│   ┌──────▼───────────────▼───────────────▼───────┐  │
│   │           RENDER PIPELINE                     │  │
│   │                                               │  │
│   │  1. Mirrored webcam background                │  │
│   │  2. Portal clip (finger quadrilateral)        │  │
│   │  3. Void fill + depth fog + grids             │  │
│   │  4. Topo ripples + head silhouette            │  │
│   │  5. 10K particle body (3 depth layers)        │  │
│   │  6. Joint rings + orbit dots                  │  │
│   │  7. Scanline + data streams                   │  │
│   │  8. HUD panel + telemetry                     │  │
│   │  9. Glitch overlay (random)                   │  │
│   │ 10. Portal border + corner markers            │  │
│   └───────────────────────────────────────────────┘  │
│                                                      │
└─────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/Axshatt/XRayVision.git
cd XRayVision

# Open in browser (no build step needed!)
open index.html
# or
python3 -m http.server 8000
# then visit http://localhost:8000
```

> **Requirements:** A modern browser with webcam access (Chrome/Edge recommended). No `npm install`, no bundler, no framework — just one HTML file.

---

## 🎮 Controls

