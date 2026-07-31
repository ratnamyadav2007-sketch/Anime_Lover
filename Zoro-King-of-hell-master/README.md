# ⚔️ ZORO — King of Hell

> *"Nothing happened."*

A cinematic, scroll-driven fan page for **Roronoa Zoro** (One Piece) — built as a **single HTML file** with vanilla JavaScript, GSAP ScrollTrigger, and the Canvas API. No frameworks, no build step. Open it and scroll.

![Made with](https://img.shields.io/badge/Made%20with-Vanilla%20JS-b34dff?style=flat-square)
![GSAP](https://img.shields.io/badge/Animation-GSAP%20ScrollTrigger-e0004d?style=flat-square)
![No Framework](https://img.shields.io/badge/Framework-None-07050d?style=flat-square)

---

## ✨ Features

### 👁️ Scroll-Scrubbed Eye Opening
- A 50-frame image sequence scrubbed by scroll position, with frame cross-blending for buttery smooth playback
- Feathered "eyelid" overlays that part as you scroll
- Lightning strikes fire at opening thresholds (28% / 62% / fully open)
- Once fully open, a light veil fades in with ghost kanji — **地獄の王** (King of Hell)

### ⚡ Realistic Lightning Engine
Not zigzag lines — a proper strike system:
- **Fractal channels** built with midpoint displacement (big kinks up high, fine detail low)
- **4-layer rendering**: wide violet corona → haze → pale sheath → white-hot core, with tapering forked branches
- **Real restrike behavior**: each strike keeps its channel and re-illuminates the *same path* 2–3 times, just like actual lightning
- **Local sky illumination** around the strike origin instead of a flat full-screen flash

### 🔊 Procedural Thunder (Web Audio API)
Three synthesized layers, no audio files:
1. A sharp high-frequency **crack** at the strike
2. A **rolling body** whose loudness wanders as it decays, with a lowpass sweep as the sound "travels"
3. A slow **sub-bass rumble** underneath

### 🗡️ Gravity Sword Drop
- Intro screen with a blurred Zoro portrait + title text that lifts and dissolves as the fall begins
- The katana hangs, accelerates with gravity easing, and **slams** down
- Speed-based motion blur, vertical stretch smear, air sway, and a fading light trail with a hot tip
- On impact: thunder strike into the blade, screen shake, shockwave — then the Zoro cut reveal with ambient crackling arcs
- Scroll input is **lerp-smoothed**, so even a fast wheel-fling plays the full fall instead of jumping to the end

### ⚔️ Slash-Split Hover Reveal
- Drag the tilted blade line across the screen to split between two artworks
- Spark particles trail the cut; fast drags call lightning down near your cursor
- Full-screen thunderstorm fires when your cursor enters the section
- Electric-border cards (a vanilla remake of the ReactBits "Electric Border" effect)

### 🎨 Extra Polish
- Slash-wipe preloader, film grain, custom cursor, live HUD clock + section state
- `prefers-reduced-motion` respected throughout
- Audio gated behind first user interaction (browser autoplay policy)

---

## 🛠️ Tech Stack

| Layer | Tool |
|---|---|
| Structure & styling | HTML5, CSS3 (custom properties, masks, blend modes) |
| Scroll animation | [GSAP 3](https://gsap.com/) + ScrollTrigger (CDN) |
| Lightning, wind, sparks, trails | Canvas 2D API |
| Thunder audio | Web Audio API (fully procedural) |
| Fonts | Pirata One · Space Mono · Shippori Mincho · Bebas Neue (Google Fonts) |

---

## 📁 Project Structure

```
├── index.html          # everything lives here — markup, styles, and scripts
├── frames/
│   ├── frame_0001.jpg  # eye-opening sequence (50 frames)
│   └── ... frame_0050.jpg
└── img/
    ├── sword.png       # falling katana
    ├── zoro_cut.png    # impact reveal artwork
    ├── zoro_dark.png   # sword-drop intro backdrop
    ├── zoro1.png       # slash split — top layer
    └── zoro2.png       # slash split — bottom layer
```

---

## 🚀 Getting Started

```bash
git clone https://github.com/Meghamittal0920/Zoro-King-of-hell.git
cd Zoro-King-of-hell
```

Then serve it locally (any static server works):

```bash
# Python
python -m http.server 8000

# or Node
npx serve
```

Open `http://localhost:8000` and scroll. That's it — no install, no build.

> **Tip:** click or scroll once before expecting sound — browsers block audio until the first user interaction.

---

## 🎛️ Tuning Knobs

A few values worth knowing if you want to remix it:

| What | Where | Default |
|---|---|---|
| Sword-fall glide smoothness | `dropFrame()` lerp factor | `0.09` (lower = floatier) |
| Eye lightning thresholds | `eyeStrikes` array | `0.28 / 0.62 / 0.96` |
| Hover-storm cooldown | `lastMoveBolt` throttle | `800ms` |
| Intro text lifetime | `clamp(p/0.16, ...)` in `applyDrop` | first 16% of scroll |
| Thunder loudness / length | `thunderSound(vol, dur)` calls | varies per strike |

---

## 🌐 Browser Support

Works in all modern browsers (Chrome, Edge, Firefox, Safari). Best experienced on desktop with a mouse for the slash-split section; touch is supported everywhere.

---

## ⚠️ Disclaimer

This is a **non-commercial fan project**. Roronoa Zoro and One Piece are the property of **Eiichiro Oda, Shueisha, and Toei Animation**. All character artwork belongs to its respective owners. The code is free to learn from and remix.

---

## 💜 Support

If this project helped or inspired you:

- ⭐ Star this repo
- 🍴 Fork it and build your own character page
- 📸 Follow me on Instagram for more builds

*Forged in Wano.* 🌊⚡
