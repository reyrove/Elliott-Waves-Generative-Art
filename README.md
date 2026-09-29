# Elliott Waves

**A seed-based generative system for financial chart compositions.**

A catalogue of computational textile compositions for fashion, textile and surface design — algorithmically drawn, seed-documented, and ready for production.

---

## Overview

Elliott Waves is a generative design system rather than a single artwork. Each composition is built from a random walk of 360 daily prices, drawn as a continuous wave line, with weekly candlesticks overlaid on top. A monthly axis runs across the bottom, and a y-axis of tick labels runs down the left.

The system is designed for:

- **Fashion houses** adapting financial ornament for apparel and accessories
- **Textile studios** developing repeat patterns and yardage
- **Surface designers** working across print, wallpaper, and interior applications

Every composition can be licensed, adapted, or commissioned to a brief.

---

## Concept

A price, when it is *traced* rather than read, becomes a wave — measured, rhythmic, quietly yours.

The financial chart — candlesticks, axes, gridlines — has always carried an unexpected beauty. It is a form of drawn computation that we look at every day without seeing it as such. Elliott Waves translates that visual language into code. Each composition begins with a random walk of daily prices and unfolds through weekly candles, monthly axes, and y-axis tick labels, producing a chart-like composition that reads as both data and decoration.

The wave path, the candle bodies, the axes, and the tick labels are all derived from a single numeric seed.

Like the other still volumes in this series (Girih, Arachne, Celestial Grove, ChaotiColor, Citrus Mosaic, Crazy Knight Curve, Crazy Knight Line, Crazy Letter, cyPollock, Digital Pollen, Draconic Fractals, Dreamscape Watercolors), **Elliott Waves is a static composition.** The plate, the framed plate, the surfaces, and the archive are all static frames. A chart is something you read; its character is stillness, not motion.

---

## Features

- **Seed-based generation** — every composition is defined by a numeric seed and can be regenerated exactly
- **Deterministic output** — the same seed always produces the same composition
- **360-day random walk** — a single continuous wave line, drawn across the frame
- **Weekly candlesticks** — 51 candles, one for every 7 days of the walk
- **Monthly axis** — 12 vertical gridlines with month labels (Jan–Dec)
- **Y-axis with tick labels** — 11 horizontal tick marks with value labels
- **Red / green candles** — bears are red, bulls are green
- **Adaptive surfaces** — one seed applied across print, scarf, textile, and wall formats
- **Archive** — eight curated seeds available for immediate loading
- **Download** — export the composition as a high-resolution PNG
- **Keyboard shortcuts** — `R` for new seed, `S` to save

---

## Project Structure

```
.
├── index.html          # Main catalogue page
├── images/
│   ├── fav.svg         # Favicon
│   ├── tote.png        # Mockup: tote bag
│   ├── tee.png         # Mockup: t-shirt
│   └── cushion.png     # Mockup: cushion
└── README.md
```

---

## How It Works

### The Seed

A numeric seed (a large integer) initializes a deterministic pseudo-random generator. From this seed, the system derives:

- Wave directions for all 360 days (alternating + and −)
- Height and width jitter factors for each daily step
- Candle body and wick jitter values for each week

Because the generator is deterministic, the same seed always produces the same composition — on any device, at any time.

### The Wave Line

The composition begins with a walk of 360 daily prices:

1. Start at the centre of the canvas (`h/2`).
2. On even days, the price moves **down**; on odd days, it moves **up**.
3. Each step's amplitude and horizontal advance are jittered by a factor between 0.8 and 1.2.

The result is a continuous wave — a single line zig-zagging across the frame, like a stock chart on a screen.

### The Candlesticks

Every 7 days — one "week" — the system draws a candlestick:

- **Open** = price at the start of the week (with jitter)
- **Close** = price at the end of the week (with jitter)
- **High** = the maximum of open and close, extended upward
- **Low** = the minimum of open and close, extended downward

If close < open, the candle is red (bearish). Otherwise it's green (bullish). The body is drawn as a filled rectangle, and the wick is drawn as a thin line through the body.

### The Axes

Two axes complete the chart:

- **Monthly axis** — 12 vertical lines, one for each month, labelled Jan through Dec. This gives the composition its sense of scale.
- **Y-axis** — a single vertical line at the left of the frame, with 11 tick marks and printed value labels. The labels are computed from the actual price range of the walk, so each composition has its own price scale.

### The Surfaces

The same seed is rendered across four surface formats. These are static frames — they represent the print-ready composition.

| Surface  | Aspect | Material          |
|----------|--------|-------------------|
| Print    | 1 : 1  | Cotton rag        |
| Scarf    | 3 : 1  | Twill silk        |
| Textile  | 4 : 3  | Fabric yardage    |
| Wall     | 2 : 3  | Wallpaper         |

Each surface uses the same underlying seed and structural logic — only the repeat, orientation, and scale change.

### Stillness

Like the rest of the still volumes, Elliott Waves does not animate. The plate is a single frozen frame — the composition is complete the moment it is generated.

This is a deliberate design choice. A chart is not a swarm. It is not a rotation. It is a plot, laid down once and left. Its stillness is what makes it print-ready in the strictest sense: what you see is what you get.

---

## Usage

### In the browser

1. Open `index.html` in any modern browser.
2. Click **New Seed** to generate a new composition.
3. Click **Download** to save the composition as a PNG.
4. Scroll to the **Archive** section and click any plate to load it into Plate 001.

### Keyboard shortcuts

| Key | Action          |
|-----|-----------------|
| `R` | New seed        |
| `S` | Save as PNG     |

### Reproducing a composition

Each composition is identified by an 8-digit seed label displayed in the metadata panel. To reproduce a specific composition, note the seed and regenerate it programmatically:

```js
const rng = new RandomGenerator(seed);
const features = buildFeatures(rng);
renderComposition(canvas, features, rng);
```

Because the generator is deterministic, this will produce the identical composition on any device.

---

## Technical Notes

- **No build step.** The system is a single HTML file with inline CSS and JavaScript.
- **No dependencies.** All drawing is done with the native Canvas 2D API.
- **Deterministic.** The `RandomGenerator` class uses a xorshift-based PRNG seeded by an integer, so identical seeds produce identical outputs.
- **Static rendering.** Every canvas renders a single frame. There is no animation loop.
- **Feature isolation.** Cover, framed plate, surfaces, and archive thumbnails each derive their own feature set from their own local RNG, without disturbing the main plate's state.
- **Pre-computed jitter.** All randomness in the wave path and candles is pre-computed in `buildFeatures` rather than drawn on the fly — so the same seed always produces the same chart across resizes.
- **Single-pass axis computation.** The y-axis tick labels are computed once from the wave's actual min/max, so the scale is always in-range and consistent.
- **Responsive.** The layout adapts from large desktop down to very small mobile devices (tested at 360px viewport width).
- **Accessible.** Supports `prefers-reduced-motion`. Pinch-zoom is enabled.

### Browser support

Tested in current versions of:

- Chrome / Edge
- Firefox
- Safari (desktop and iOS)

---

## Licensing

All Elliott Waves compositions are **seed-documented** and available for licensing across textile, surface, and print applications.

- **Standard licenses** cover single-product production runs.
- **Commercial use, custom editions, or exclusive rights** are available on request.

Each license is issued against a specific seed ID. Regeneration of the same seed produces the identical composition — ensuring reproducibility between artist, studio, and manufacturer.

For licensing enquiries: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Commission

Elliott Waves is a generative design system, not a fixed artwork. It can be adapted for specific briefs:

| Service     | Description                                                       |
|-------------|-------------------------------------------------------------------|
| Licensing   | Existing seeds from the archive, licensed for production use      |
| Commission  | New compositions designed to your palette, repeat, and product    |
| Systems     | A private generative tool built for your studio's ongoing use     |

To begin a conversation: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Series

Elliott Waves is part of a computational textile series. Each volume approaches ornament from a different structural angle:

| Volume                     | Structure                    | Motion                     |
|----------------------------|------------------------------|----------------------------|
| Girih 1                    | Islamic geometric            | Static                     |
| Arachne                    | Rotating rings               | Static                     |
| Baroque Me Baby            | Baroque frames               | Static                     |
| Bezier 1                   | Concentric curves            | Static                     |
| Bezier 2                   | Single rotating curve        | Animated (plate)           |
| Brownian Graphe            | Graph networks               | Animated + interactive     |
| Celestial Grove            | Recursive branch trees       | Static                     |
| ChaotiColor                | Cellular automata            | Static                     |
| Citrus Mosaic              | Arc-and-triangle tiles       | Static                     |
| Crazy Knight Curve         | Knight's-tour smooth path    | Static                     |
| Crazy Knight Line          | Knight's-tour gradient       | Static                     |
| Crazy Letter               | Framed wavy lines            | Static                     |
| cyPollock                  | Scattered branch field       | Static                     |
| Digital Pollen             | Noise-driven texture         | Static                     |
| Draconic Fractals          | Tiled dragon curve           | Static                     |
| Dreamscape Watercolors     | Layered watercolor blooms    | Static                     |
| **Elliott Waves**          | **Financial chart**          | **Static**                 |

The series is designed as a coherent whole — same page structure, same seed logic, same licensing and commission terms — so that each volume can be presented individually or as part of a larger body of work.

---

## Credits

- **Design & Generative System** — Reyhaneh Daneshdoost
- **Typefaces** — Cormorant Garamond · DM Mono
- **Platform** — Reyrove Studio
- **Edition** — Elliott Waves, Autumn 2026

### On AI tools

Where technical obstacles were encountered, AI tools were used for debugging and code optimization. Every structural, aesthetic, and conceptual decision remained the artist's own.

---

## Links

- Website — [reyrove.github.io](https://reyrove.github.io/)
- Instagram — [@rey._.rove](https://www.instagram.com/rey._.rove/)
- LinkedIn — [Reyhaneh Daneshdoost](https://www.linkedin.com/in/reyhaneh-daneshdoost-730481160/)
- X — [@reyrove](https://x.com/reyrove)

---

© Elliott Waves · All compositions reproducible by seed · Computational Textile Design