# ピカチュウ · PIKACHU

A single-section React (Vite) page: Pikachu sits dead centre, leans toward your cursor with
spring smoothing, and plays a giggle + thunder reaction when you click him — over a WebGL
fluid splash cursor and a falling katakana glyph rain.

```bash
npm install
npm run dev      # http://localhost:5173
npm run build
```

## What's in it

| Piece | File | Notes |
| --- | --- | --- |
| Fluid cursor | `src/components/SplashCursor.jsx` | React Bits `SplashCursor`, tinted `#FFCB05` (`RAINBOW_MODE={false}`) |
| Glyph rain | `src/components/GlyphRain.jsx` | Canvas katakana columns, DPR-aware, pauses when the tab is hidden |
| Pikachu | `src/components/Pikachu.jsx` | Canvas sprite playback from the frame atlas |
| Thunder | `src/components/Lightning.jsx` | Full-screen yellow bolts on click, drawn with midpoint displacement |
| Theme | `src/App.jsx` (`.stage__theme`) | ☀/☾ chip, top right - dark night by default, light studio plate optional, remembered in `localStorage` |
| Section + type | `src/App.jsx`, `src/index.css` | Noto Sans JP for ピカチュウ, Titan One styled as the Pokémon wordmark |

## Frames

`pikachu.zip` (75 PNGs, 1280x720, grey studio plate) was keyed and packed into one WebP atlas
in `public/frames/`:

* `pikachu-char.webp` - the background flood-filled away, cropped to him with 22 px of padding
  so his ears never touch a cell edge.
* `pikachu-char.half.webp` - half-resolution copy, loaded on narrow or low-DPR screens.
* `frames.json` - atlas geometry, crop rect and segment ranges the renderer reads.

Segments the renderer uses (0-indexed atlas frames):

| Range | What it is |
| --- | --- |
| 20 | facing front |
| 9 | head turned toward screen-right |
| 31 | head turned toward screen-left |
| 3-4 | eyes closing, then shut - the source's own blink |
| 44-56 | the giggle, stopped right before the source starts throwing bolts |

## Behaviour

* **Look direction follows the cursor's position**: left half - looks left, right half - looks
  right, middle band - faces front. A 0.20/0.14 hysteresis band plus a 150 ms dwell means
  sweeping from one side to the other does not flash a turn while crossing the centre.
* **Turns are covered by a blink**, the same cheat the source animation uses, followed by an
  80 ms cross-dissolve. He also blinks on his own every few seconds while facing front.
* **The body stays centred** - at most 11 px of spring-damped lean toward the cursor.
* **Click him** and he giggles while full-screen yellow lightning cracks across the stage,
  regrown with fresh jitter every 55 ms so it crackles rather than sitting still.
* `prefers-reduced-motion` renders one static frame, skips the rain and suppresses the thunder.
