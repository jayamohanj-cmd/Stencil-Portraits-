# Spray Paint Portraits — 3-Layer Stencil Maker

Turn any photo into **three cuttable stencil layers** — silhouette, mid-tones and details — ready to print and cut by hand, or send to a **laser cutter or Cricut** as vector SVG files. Built for the classic classroom *spray paint portraits* project: cut one stencil per layer, then spray lightest → darker → darkest to reveal the portrait.

Everything runs in a single HTML file, entirely in your browser. **No installation, no server, no uploads — photos never leave your computer.**

## Getting started

1. Download `stencil-maker.html` (or clone this repo).
2. Double-click the file — it opens in any modern browser (Chrome, Edge, Firefox, Safari).
3. Drop in a photo (or paste with `Ctrl+V`). Portraits with a plain background work best.
4. Tweak, then print or download your cut files.

Works offline once saved. Nothing else in this repo is required to run it.

## Features

### Three-layer separation
The photo is converted to grayscale and split into three layers by **value thresholds**, each with its own slider:

| Layer | Pass | What it captures |
|---|---|---|
| 1 · Silhouette | base layer, sprayed first | the whole shape — lightest values |
| 2 · Mid-tones | second pass | medium values |
| 3 · Details | final pass | darkest shadows and features |

A live composite preview shows the finished piece in your chosen spray colours (canvas + three layer colours, all pickable).

### Built for cuttability
- **Smoothing** — softens edges into knife-friendly shapes.
- **Speck removal** — deletes dots and pinholes too small to cut.
- **Floating-piece detection** — any white area fully enclosed by a cut region (eyes, highlights) would fall out of a real stencil. These are found automatically and highlighted in red.
- **Auto-bridges** — one click adds thin ties that anchor each floating piece through the thinnest part of the surrounding cut area, with adjustable bridge width. Bridges are shown in blue in the previews and included in every export. Turn them off if students should plan pen bridges by hand.
- **Registration marks** — identical ✚ marks cut into all four corners of every layer so the passes line up on the canvas.

### Output options
- **Print** — each layer on its own page, straight from the browser.
- **PNG** — raster downloads of each layer.
- **SVG (vector)** — true traced cut paths, not embedded bitmaps, so Adobe Illustrator, Cricut Design Space, and laser software treat them as editable, cuttable shapes. Two styles:
  - *Filled shapes* — for Cricut / Silhouette
  - *Hairline red outlines* — for laser cutters
  
  A width setting (80–600 mm) controls the real-world size the SVG opens at; all three layers export at identical dimensions for registration.

## Classroom workflow

1. **Cut.** Print each layer and cut out the **black** areas with a craft knife — or send the SVGs to a laser cutter or Cricut. The black areas are the openings the paint passes through.
2. **Silhouette pass.** Tape layer 1 to the canvas and spray the **lightest** colour. Lift carefully.
3. **Mid-tone pass.** Line up layer 2 on the registration marks and spray the **darker** colour. Wait ~10 minutes between coats.
4. **Detail pass.** Line up layer 3 and spray the **darkest** colour. Reveal the portrait!

> **Tip:** a bridge in the silhouette layer blocks the spray there, leaving a thin unsprayed stripe — that's normal stencil practice. Touch it up after lifting the stencil.

## How it works

All processing is client-side JavaScript on a `<canvas>`:

- Grayscale conversion with brightness/contrast/blur via canvas filters, then per-layer thresholding.
- Despeckling and floating-piece detection by connected-component flood fill.
- Bridges are routed with a breadth-first search through the cut region, so each tie crosses at the thinnest point.
- SVG export traces pixel boundaries into closed loops (clockwise around openings, counter-clockwise around holes, even-odd fill), then simplifies them with collinear merging and Ramer–Douglas–Peucker.

No frameworks, no build step, no dependencies — one self-contained HTML file. The Google Fonts link is the only network request, and the app degrades gracefully without it.

## License

Free to use and adapt for your classroom. If you publish a fork, a link back is appreciated.
