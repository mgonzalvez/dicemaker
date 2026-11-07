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
9. Theme changes must update both DiceMaker’s local appearance rules and TokenMaker’s `html[data-theme]` variables. Test new panels, menus, dialogs, previews, and exports in light and dark appearance.

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

## Appearance maintenance

`setTheme()` in `app.js` is the single theme entry point. It synchronizes the saved DiceMaker preference, `body.dark` compatibility styling, and the `html[data-theme]` value required by `tokenmaker-base.css`. Put DiceMaker-only dark-surface adjustments in `tokenmaker-overrides.css`; do not add isolated dark-mode behavior that bypasses this path.

## Checks

Run before a commit:

```bash
node --check app.js
```

## Registry & provenance rule (portfolio-wide)

Personal project — completely separate from Apple work.

- `.npmrc` pins `registry=https://registry.npmjs.org`. Never let Apple's internal npm mirror (`npm.apple.com`, `artifacts.apple.com/artifactory/...`) end up in `package-lock.json`; GitHub Actions can't reach it and CI fails with `ENOTFOUND`.
- Audit before pushing: `../scripts/check-registry.sh` (add `--fix` to normalize).
- No work credentials, internal hostnames, proprietary assets, or confidential material in this repo.
