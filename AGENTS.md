# DiceMaker Contributor Notes

## Stack

DiceMaker is a static, framework-free browser application. It has no package installation, build step, or backend. Serve the repository over HTTP for local use because the browser loads bundled SVG files.

## Critical rules

1. Reuse TokenMaker components, layout conventions, icon handling, and attribution patterns whenever they fit. DiceMaker uses local standalone copies of the needed styles and icon assets; do not reintroduce a runtime dependency on `TokenMaker/`.
2. The D6 physical relationships are fixed: faces 1/6, 2/5, and 3/4 are opposite. Custom artwork must never change this mapping.
3. All active templates on a preview or exported PDF page must be centered horizontally and vertically based on the actual template count on that page.
4. Template quantities are constrained to the current page capacity. Recalculate this capacity after changing paper, orientation, gutter, margin, tabs, or die size.
5. Keep Fractal Symbols attribution in the page footer, license dialog, and printable PDF footer.
6. Keep user artwork serializable in saved project JSON. SVG uploads must be sanitized before insertion into the document.
7. Keep the app static and client-side. Do not add a server, telemetry, accounts, or a build dependency without explicit approval.
8. Keep the guided tutorial aligned with the actual UI and workflow. It is implemented in `app.js` with TokenMaker-style spotlight and callout classes supplied by `tokenmaker-base.css`.

## Key files

- `index.html` — application markup
- `app.js` — editor state, SVG rendering, D6-template layout, project save/load, and exports
- `styles.css` — DiceMaker-specific rules
- `tokenmaker-base.css` — local TokenMaker visual-system base
- `tokenmaker-overrides.css` — TokenMaker visual-system reuse and D6 mappings
- `icon-manifest.js` — generated icon metadata; do not hand-edit
- `assets/icons/` — runtime Fractal Symbols artwork and upstream license files
- `favicon.svg` — DiceMaker browser icon
- `ATTRIBUTION.md` — artwork attribution details

## Tutorial maintenance

The guided tutorial is intentionally a UI tour, not a static help dialog. Each step names a live selector and design/build workspace. If markup or workflow changes, verify every tutorial target still exists and update the title and copy in the `tutorialSteps` collection in `app.js`.

## Checks

Run before a commit:

```bash
node --check app.js
```
