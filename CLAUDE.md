# SPS Lab — Landing Page & Maker Preview Workspace

A lightweight static site for previewing landing pages, maker tool prototypes, and app mockups for Social Print Studio. Hosted on Vercel. Internal use for team sharing and proof of concepts.

## Architecture

**Pure static HTML/CSS/JS.** No build step, no framework, no bundler. Each project is a self-contained folder with its own `index.html`. The root `index.html` is the gallery menu linking to all projects.

```
sps-lab/
├── index.html              ← Gallery menu (the hub)
├── projects/
│   ├── demand-engine/      ← Demand engine test landing pages
│   │   ├── babys-first-year/
│   │   │   └── index.html
│   │   ├── gift-tiny-books/
│   │   │   └── index.html
│   │   └── homepage-identity/
│   │       ├── calendar-co.html
│   │       ├── gift-co.html
│   │       └── control.html
│   ├── mothers-day/        ← Mother's Day 2026 campaign pages
│   ├── makers/             ← Maker tool prototypes
│   └── mockups/            ← App mockups and interactive walkthroughs
├── shared/                 ← Shared assets (fonts, base CSS, images)
└── CLAUDE.md
```

## Adding a New Project

1. Create a folder under the appropriate `projects/` subdirectory
2. Build a self-contained `index.html` (inline CSS/JS is fine — these are previews, not production)
3. Add a card to the root `index.html` gallery linking to the new page
4. Each project card needs: title, short description, and a tag (landing / maker / mockup / experiment)

## Design Conventions

- **Fonts:** Instrument Serif (headings) + Hanken Grotesk (body) — loaded from Google Fonts
- **Colors:** Neutral palette (`#f5f4f1` bg, `#1a1a1a` text, `#c45d3e` accent)
- **Style:** Clean, minimal, generous whitespace. Match SPS brand aesthetic — modern without being trendy
- **Images:** Use SPS product photography from the CDN (`cdn.shopify.com/s/files/1/0366/...`) or placeholder images
- **Responsive:** All pages should work on mobile. Grid → single column at 640px.

Individual project pages can have their own design — they're previews of different concepts. The gallery menu stays consistent.

## Card Tags

Use these tags on the gallery cards:
- `tag-landing` (green) — Landing pages for ads/campaigns
- `tag-maker` (blue) — Maker tool / product customizer UIs
- `tag-mockup` (purple) — App mockups and interactive walkthroughs
- `tag-experiment` (orange) — Experiments and test concepts

## Card HTML Template

```html
<a href="projects/[category]/[name]/index.html" class="card">
  <span class="card-arrow">&rarr;</span>
  <div>
    <div class="card-title">Project Name</div>
    <div class="card-desc">One-line description of what this preview shows.</div>
  </div>
  <span class="card-tag tag-landing">Landing</span>
</a>
```

Replace the corresponding `<div class="empty-card">...</div>` in the gallery when adding a real project.

## SPS Product Data

**printkit.dev** is SPS's developer API for photo printing. The product catalog is useful as a reference when building landing pages and mockups:

- **Full catalog:** `https://printkit.dev/products.json` — all products with titles, descriptions, sizes, price ranges, and CDN image URLs
- **Per-product detail:** `https://printkit.dev/products/{handle}.json` — variant-level SKUs, specs, constraints

Current products in the catalog (6 as of Feb 2026, more being added):
- `large-format-prints` — 20 sizes, $9-60
- `gallery-frames` — 19 sizes, $54-289 (white/black/natural wood)
- `wood-prints` — 21 sizes, $22-322
- `acrylic-photo-block` — 4 sizes, $40-54
- `metal-prints` — 25 sizes, $21-406
- `photo-magazine` — 38 pages, $26

**Not all SPS products are in printkit yet.** Major products missing from the API but sold on socialprintstudio.com:
- Daily Calendar ($1.67M/yr — the #1 product)
- Tiny Books ($875K/yr — #2)
- Layflat Guestbook ($650K/yr — #3)
- Photo Magnets, Classic Prints, Wedding Albums, etc.

When building landing pages, use printkit.dev for product images and specs where available. For products not yet in the API, pull images from the Shopify CDN (`cdn.shopify.com/s/files/1/0527/1502/8643/...`) or socialprintstudio.com product pages.

## Context

This lab supports the strategies in `/Users/georgesylvain/claude/`:
- `demand-engine-testing-plan.md` — 4 demand engine tests (Baby's First Year, Homepage Identity, Gift Positioning, AI Annual Book)
- `mothers-day-2026-strategy.md` — 6-play Mother's Day blitz with landing page needs
- `2026-sps-strategy.md` — Master strategy with priority stack

## Hosting

- **Repo:** `gsylvain/sps-lab` on GitHub
- **Hosting:** Vercel (connected to repo, auto-deploys on push)
- **Shareable URLs:** Each project gets a clean URL like `sps-lab.vercel.app/projects/demand-engine/babys-first-year/`
