# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**The Ranch House Bragadiru** — direct booking website for a vacation rental property.
- Domain: `cazarebragadiru.ro` (GitHub Pages, CNAME configured)
- Listed on Booking.com (score 9.5) and Airbnb (score 5/5)
- Phone & WhatsApp: `+40726420648`
- Address: Strada Iederei nr 65, Bragadiru, Ilfov, 077025

## Architecture

Single-page static site — no build step, no framework, no dependencies except one Google Fonts request.

- **`index.html`** — entire site: all HTML, CSS (in `<style>`), JS (in `<script>`), and two Schema.org JSON-LD blocks
- **`images/`** — 19 photos, currently `.jpg`; will be converted to `.webp` (the `<picture>` elements already reference both formats with `.webp` as source and `.jpg` as fallback)
- **`sitemap.xml`** — single URL; update `<lastmod>` after content changes
- **`robots.txt`** — allows all agents
- **`CNAME`** — `cazarebragadiru.ro`

## Image Files

```
hero.jpg           ← exterior front (also used as CSS hero background)
exterior-1/2/3.jpg ← house front, covered parking, side view
garden-1/2/3.jpg   ← BBQ+hammock, flowers, swing under tree
living-1/2/3.jpg   ← living room
kitchen-1/2/3.jpg  ← kitchen
bedroom-1-1/2.jpg  ← bedroom 1
bedroom-2-1/2.jpg  ← bedroom 2
bathroom-1/2.jpg   ← bathrooms
```

When `.webp` files are added, the gallery `<picture>` elements will automatically prefer them. The hero CSS background in `.hero {}` still references `.jpg` — update that line manually once `hero.webp` exists.

## Site Sections (in order)

1. Topbar — phone + WhatsApp links
2. Sticky nav — brand + links + "Rezervă acum" CTA
3. Hero — CSS background with dark overlay, ratings badges, CTA buttons
4. Quick facts bar — bedrooms, baths, capacity, garden, parking, location
5. `#galerie` — 9-photo grid + lightbox (all 18 photos accessible via lightbox)
6. `#facilitati` — 9 amenity cards
7. `#tarife` — weekday (342 lei) / weekend (420 lei) pricing cards
8. `#locatie` — location points list + Google Maps iframe embed
9. `#faq` — 9 FAQ items, JS accordion
10. `#contact` — phone + WhatsApp cards, contact details, platform badges
11. Footer

## Key Implementation Details

- **Gallery**: first 9 photos shown in grid (first item spans 2×2); all 18 accessible in lightbox. Data lives in the `PHOTOS` array in the `<script>` block — add/remove photos there.
- **FAQ**: data lives in the `FAQS` array — add/remove questions there.
- **Platform links** (Booking.com + Airbnb) in the contact section use search URLs as placeholders — replace with exact listing URLs when available.
- **No contact form** — phone/WhatsApp only. A form (FormSpree) is planned for a future phase.
- **Fonts**: Playfair Display (Google Fonts) for headings; `system-ui` for body.
- **Colour palette**: warm browns (`#5C3D1E`, `#3E2810`), cream (`#F5ECD7`), sage (`#4A6741`), aged gold (`#8B6914`).
- **Responsive breakpoints**: 900px (tablet — nav collapses, 2-col grid) and 600px (mobile — single column).

## Development

No build step — open `index.html` directly in a browser. Deploy by pushing to `main`.
