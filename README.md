# DiceMaker

DiceMaker is a static, browser-based print-and-play D6 design tool. Customize six independent faces with bundled Fractal Symbols or uploaded artwork, then arrange foldable dice templates on US Letter or A4 PDF sheets.

All design, image processing, project saving, and PDF creation run locally in the browser. DiceMaker has no accounts, analytics, server component, or build step.

## Features

- Six independently editable faces, each with custom artwork, colors, icon outline, rotation, scale, and optional text
- A standard white D6 with black pips as the starting point and reset preset
- Fixed conventional D6 opposites: 1 ↔ 6, 2 ↔ 5, and 3 ↔ 4
- Searchable Fractal Symbols icon library plus SVG, PNG, and JPG uploads
- Randomize all six face icons
- 10, 12, 14, 16 (default), and 19 mm face sizes
- Optional glue tabs; cut-and-fold or cut-only guides
- Mixed custom dice templates, page-fill controls, Letter/A4, and portrait/landscape layouts
- Centered print layouts and 300 DPI PNG/PDF export
- JSON project save/load, light/dark appearance, and a first-visit guided UI tutorial

## Run locally

Serve the repository over HTTP so the browser can load the bundled SVG artwork:

```bash
python3 -m http.server 8766
```

Then open <http://localhost:8766/>.

## Project layout

| Path | Purpose |
| --- | --- |
| `index.html` | Application interface and page entry point |
| `app.js` | D6 editor, template layout, project persistence, and exports |
| `styles.css` | DiceMaker-specific styling |
| `tokenmaker-base.css` | Local copy of the TokenMaker visual system |
| `tokenmaker-overrides.css` | Reused TokenMaker interaction and layout rules |
| `icon-manifest.js` | Generated searchable icon metadata |
| `assets/icons/` | Bundled Fractal Symbols SVG/PNG artwork and upstream license files |
| `favicon.svg` | DiceMaker D6 browser icon |
| `ATTRIBUTION.md` | Third-party artwork attribution |

`TokenMaker/` may exist locally as a development reference, but is deliberately ignored by Git. DiceMaker loads only the standalone runtime copies listed above, so a fresh repository clone remains fully functional.

## Workflow

1. Start from the standard pip D6 or select **Load standard D6 pips**.
2. Select each of the six face tabs and customize its artwork, colors, and optional text. Use **Randomize all face icons** for a quick icon-based starting point.
3. Save the completed die to the project. Repeat to add other custom dice.
4. Select **Build printable sheet**, set quantities up to the live page capacity, then configure paper, margins, gutter, tabs, and guides.
5. Review the centered template preview and export a 300 DPI PDF.

Use the **Tutorial** button in the header at any time for a step-by-step tour of this workflow.

## Validation

Run the basic source check before committing:

```bash
node --check app.js
```

## Artwork attribution

The bundled artwork is **Fractal Symbols: Board Game Library** by Felix Thalin, licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). DiceMaker retains the required attribution in its interface and printable PDF footer. See [ATTRIBUTION.md](ATTRIBUTION.md) and the license files in `assets/icons/`.
