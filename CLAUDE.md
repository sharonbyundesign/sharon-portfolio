# CLAUDE.md

Guidance for working in this repository.

## What this is

A static personal portfolio site for Sharon Byun (Senior Product Designer). No
build step, no framework, no package manifest — just hand-authored HTML files
with inline CSS and vanilla JS.

- `index.html` — the home page. Single self-contained file: all CSS lives in one
  `<style>` block in `<head>`, all JS in `<script>` tags before `</body>`.
- `about.html` — the about page.

There is no `package.json`, bundler, or test suite. Edits are made directly to
the HTML files.

## Running a local preview

The site is plain static files, but `python3 -m http.server` is blocked in this
environment (sandbox `PermissionError`). Use `npx serve` instead:

```
npx serve -l 3456 .
```

A `.claude/launch.json` is configured to run exactly this for the browser
preview tool.

## Architecture notes

### Hero particle animation (`index.html`)
- A canvas (`#phCanvas`) renders ~9000 particles that assemble into the headline
  text "I make complex / things feel / inevitable." as the user scrolls.
- The effect is scroll-driven: `.hero-scroll-wrap` is tall (`320vh`) with a
  sticky inner `.hero-sticky`; scroll progress (`currentT`, 0→1) drives how far
  particles have converged on their text targets.
- `sampleText()` rasterizes the headline to an offscreen canvas and samples
  opaque pixels as particle targets. Sampling step size controls density (step
  of 1 = dense/legible, larger = sparser).
- The "Scroll" affordance (`#scrollHint`) is centered in the hero viewport and
  fades out as the user scrolls.

### Work section
- Three `.case-card`s, each opening a detail modal via `openModal(key)`. Modal
  content is defined in the `modals` object in the script — edit copy there.
- Each card has an SVG diagram thumbnail (state machine, funnel, Venn) plus a
  particle-dot overlay (`.case-card-visual::after`, a `radial-gradient` dot
  pattern) that ties the thumbnails to the hero's stippled aesthetic.
- Hover state is intentionally subtle: a light warm tint (`#EAE6E0`), NOT a dark
  inversion. Keep text dark on hover for legibility.

### Design system
- Colors, fonts, and weights are defined as CSS custom properties in `:root`.
  Reuse these variables rather than hardcoding hex values.
- Fonts: Cormorant Garamond (serif, headlines) and Inter (sans, body), loaded
  from Google Fonts.
- Do NOT add Unsplash or other external stock photography — the visual language
  is geometric SVG diagrams plus particle/dot textures.

## Conventions
- Keep everything in the single-file-per-page structure; don't introduce a build
  step or split CSS/JS into separate files unless asked.
- Respect `prefers-reduced-motion` (already handled via a media query).
- `.DS_Store` files and `.claude/launch.json` are local artifacts — keep them out
  of commits.

## Git / PRs
- Default branch is `main`. Branch off it for changes rather than committing to
  `main` directly.
- The repo is owned by the `sharonbyundesign` GitHub account. Note that the
  `gh` CLI may be authenticated as a different user (`sharon-byun`) that is not a
  collaborator, in which case `gh pr create` fails with "must be a
  collaborator" — fall back to the token in the git remote.
