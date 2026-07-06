# PLM Media Kit

## What we're building
A single, self-contained, scrollable web page (`index.html`) that replaces the 2026 Peter Lohmann
sponsorship & media kit PDF with an interactive "Apple-style" microsite. It will be hosted at a URL
like `sponsor.peterlohmann.com` and linked from Squarespace (also works embedded in an iframe).

## The one rule that matters most
All prices, availability, dates, and deals live in a single `CONFIG` object at the top of the
`<script>` in `index.html`. **You never edit layout or logic to change a price** — you only edit CONFIG.
Bundle prices and savings badges are *computed* from line items, so numbers can never drift.

## How to update (plain English)
- **Change a price** → edit the number in `CONFIG.products` / `seasonPrograms` / `consulting`.
- **Podcast comes back** → set `CONFIG.podcast.available = true`. Everything un-grays and podcast
  slots automatically rejoin the bundle math. (Return date lives in `CONFIG.podcast.returnDate`.)
- **Add / remove an urgent deal** → edit the `CONFIG.urgentDeals` array.
- **Swap a logo or the headshot** → search the file for `SWAP:` and set the image `src`.

## Files
- `index.html` — the entire page (inline CSS + JS, no build step, no framework, no dependencies).
- `CLAUDE.md` — this file.

## Structure of index.html
1. Top comment block: "How to update this page".
2. `CONFIG` object — the only thing a non-developer edits.
3. Compute engine — pure functions (`computeBundle`, `roundUpTo`, `productCounts`, etc.).
4. Self-check — asserts the pricing validation targets in the console (dev only).
5. Rendered sections (hero, about, audience charts, engagement, pricing, bundles, deals, consulting, CTA).

## Validation targets (must always hold)
- Podcast OFF: Momentum = $3,610/mo · Market Domination = $6,365/mo.
- Podcast ON:  Momentum = $5,195/mo · Market Domination = $9,160/mo.
- Momentum badge = 24% savings · Market Domination badge = 33% savings (both states).

## Current status
- Podcast is currently **sold out** until **November 12, 2026** (`CONFIG.podcast.available = false`).
- GitHub: pushed to the user's account (`andrewmswensen-hue`) under repo `plm-media-kit`.

## Constraints (don't break these)
- No external runtime dependencies; must work opened directly (`file://`) and when hosted.
- No `localStorage`/`sessionStorage`. All state comes from CONFIG at load.
- Responsive; `prefers-reduced-motion` disables all scroll animation.
- No real brand-logo recreations and no real sponsor ad copy — stylized placeholders only.
