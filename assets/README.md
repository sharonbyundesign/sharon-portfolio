# Assets

Drop images and media here, organized by use.

```
assets/
├── case-studies/
│   ├── enterprise-approval-workflow/   # Card 01 — Blaze AI
│   ├── certifications-badges/          # Card 02 — Skillshare
│   └── creator-hub-integration/        # Card 03 — Skillshare
├── about/                              # Portrait, timeline images, fun-facts
└── shared/                             # Logos, favicons, OG/social images
```

## Referencing assets in HTML

Use a path relative to the page (both `index.html` and `about.html` live at the
repo root):

```html
<img src="assets/case-studies/certifications-badges/hero.png" alt="…" />
```

## Conventions
- Use lowercase, hyphenated filenames (`approval-states.png`, not `Approval States.png`).
- Prefer optimized web formats — `.webp` or compressed `.jpg`/`.png`; `.svg` for diagrams.
- The `.gitkeep` files just keep empty folders tracked in git; delete them once a
  folder has real assets.
