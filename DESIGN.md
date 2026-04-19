# One Gate — Design System

B2B sourcing & logistics gateway. Tone: **minimal, premium, high-trust**. Every decision should feel clean, spacious, and strategic.

---

## Color Palette

Defined as CSS custom properties in `src/layouts/Layout.astro`.

| Token | Hex | Usage |
|---|---|---|
| `--forest` | `#18442A` | Primary brand, CTAs, headings, icons |
| `--leaf` | `#45644A` | Hover states, secondary accents |
| `--wood` | `#816645` | Tertiary accents, warm highlights |
| `--sand` | `#E4DBC4` | Nav links on dark bg, sub-accents |
| `--off-white` | `#F3EDE3` | Section backgrounds, logo fill, button bg on dark |
| `--ocean` | `#83918F` | Muted text, secondary tags |
| `--white` | `#FFFFFF` | Page background, card surfaces |

### Dark surface palette (navbar scrolled, footer, hero overlay)
- Deep forest: `#0a1a10` (footer bg)
- Dark overlay: `rgba(10, 26, 16, 0.92–0.97)` (navbar scrolled, hero gradient)

### Text colors
- Headings on light: `#0c1c12`
- Body on light: `#5c6660`
- Muted on light: `#6a7870`
- Links on dark surface: `rgba(243, 237, 227, 0.75)` (sand at 75%)

---

## Typography

Loaded via Google Fonts in `src/layouts/Layout.astro`.

| Role | Font | Weight |
|---|---|---|
| Headings `h1–h6` | **Montserrat** | 700–800 |
| Navigation, labels, buttons | **Montserrat** | 500–700 |
| Body copy, descriptions | **Raleway** | 400–500 |
| Subheadlines, captions | **Raleway** | 300–400 |

### Type scale

| Element | Size | Weight | Notes |
|---|---|---|---|
| H1 hero | `clamp(2.6rem, 4.5vw, 4rem)` | 800 | Letter-spacing `-0.025em` |
| H2 section | `clamp(2rem, 3vw, 2.8rem)` | 800 | Letter-spacing `-0.02em` |
| H3 card title | `0.92–1.05rem` | 700 | |
| Eyebrow label | `0.7rem` | 700 | Uppercase, `letter-spacing: 0.14em` |
| Body | `1rem` | 400 | Line-height `1.78` |
| Small / meta | `0.75–0.85rem` | 400–500 | |
| Button | `0.82–0.9rem` | 600–700 | `letter-spacing: 0.04em` |
| Nav links | `0.85rem` | 500 | `letter-spacing: 0.02em` |

---

## Spacing

Max content width: **1160px**, centered with `margin: 0 auto`.

| Token | Value | Usage |
|---|---|---|
| Page padding | `0 2.5rem` | All sections left/right |
| Section padding | `9rem 2.5rem` | Standard tall sections |
| Section padding (short) | `7rem 2.5rem` | Tighter sections |
| Card padding | `1.75–2rem` | Inner card spacing |
| Gap (grid) | `1.25–1.5rem` | Card/pillar grids |
| Gap (layout) | `5–6rem` | Two-column layouts |

---

## Components

### Navbar

File: `src/components/Navbar.astro`

- **Default (hero):** Fully transparent, overlaps the full-viewport hero map
- **Scrolled (>10vh):** `rgba(12, 28, 18, 0.97)` + `backdrop-filter: blur(16px)` — dark forest
- **Height:** `80px`
- **Logo:** `/public/logo.svg` at `52px` height — fills are `#F3EDE3` (off-white), no CSS filter needed
- **Nav links:** Off-white on both states, hover → `--sand`
- **CTA button:** Background `--off-white`, text `--forest`, pill shape (`border-radius: 50px`)
- Transition on all state changes: `0.35s ease`

### Buttons

Two variants used across the site:

**Primary (dark bg context — hero)**
```css
background: var(--sand);
color: var(--forest);
border-radius: 50px;
padding: 0.9rem 2.2rem;
font: 700 0.9rem Montserrat;
letter-spacing: 0.04em;
```
Hover: `background: white`, `translateY(-2px)`, shadow `0 10px 28px rgba(0,0,0,0.2)`

**Primary (light bg context — sections)**
```css
background: var(--forest);
color: white;
border-radius: 50px;
padding: 0.85–0.9rem 2–2.2rem;
font: 700 0.9rem Montserrat;
```
Hover: `background: var(--leaf)`, `translateY(-2px)`, shadow `0 8–12px 24–32px rgba(24,68,42,0.22–0.24)`

**Navbar CTA**
```css
background: var(--off-white);
color: var(--forest);
border: 1px solid var(--off-white);
border-radius: 50px;
padding: 0.55rem 1.4rem;
```

### Section Eyebrow Labels

Pattern used before every section heading:
```css
font: 700 0.7rem Montserrat;
letter-spacing: 0.14em;
text-transform: uppercase;
color: var(--forest);
```
No background chip — just the text, no extra decoration.

### Cards

**Feature / pillar cards (light sections)**
```css
background: white;
border-radius: 18px;
padding: 1.75rem;
border: 1px solid rgba(24, 68, 42, 0.07);
```
Hover: `translateY(-3px)`, `box-shadow: 0 10px 30px rgba(24,68,42,0.09)`

**Floating cards (over dark/map backgrounds)**
```css
background: rgba(255,255,255,0.96);
backdrop-filter: blur(12px);
border-radius: 14px;
padding: 0.85rem 1.2rem;
border: 1px solid rgba(24,68,42,0.1);
box-shadow: 0 6px 24px rgba(0,0,0,0.14);
```

**Value blocks (off-white sections)**
```css
background: var(--off-white);
border-radius: 20px;
padding: 2rem;
border: 1px solid rgba(24,68,42,0.06);
```

### Card Icons

Square icon containers used in cards and pillars:
```css
width: 40–52px;
height: 40–52px;
background: rgba(24, 68, 42, 0.07–0.09);
border-radius: 11–14px;
color: var(--forest);
```

---

## Section Layouts

### Hero
- Full viewport (`height: 100vh`)
- Leaflet map (CartoDB Positron tiles) fills 100% as `position: absolute`
- Dark forest gradient overlay: `100deg`, from `rgba(10,26,16,0.92)` left → transparent right
- Content: left-aligned at `max-width: 560px`, vertically centered
- Floating cards: `position: absolute`, bottom-right, column stack
- Navbar overlaps (no padding-top offset)

### Two-column sections (About)
- `grid-template-columns: 1fr 1fr`, `gap: 6rem`
- Left: eyebrow + heading + body copy
- Right: large value blocks

### Centered header + grid (Solutions)
- Section header centered, `max-width: 620px`
- Platform mockup full-width below
- 4-column pillar grid below mockup

### Final CTA
- Centered, `max-width: 560px`
- Just heading + single button
- Padding: `10rem 2.5rem` (extra generous whitespace)

---

## Section Backgrounds

Alternating backgrounds create rhythm without harsh contrast:

| Section | Background |
|---|---|
| Hero | Full-viewport map + dark overlay |
| About | `white` |
| Solutions | `#f5f7f6` (very light grey-green) |
| Final CTA | `white` |
| Footer | `#0a1a10` (deep forest) |

---

## Border Radius

| Context | Radius |
|---|---|
| Large cards / sections | `18–28px` |
| Standard cards | `14–18px` |
| Icon containers | `9–14px` |
| Buttons / pills | `50px` |
| Tags / chips | `50px` |
| Inputs | `10px` |
| Map mockup browser | `18px` |
| Tooltip labels | `6px` |

---

## Shadows

| Context | Shadow |
|---|---|
| Floating card (on dark) | `0 6px 24px rgba(0,0,0,0.14)` |
| Card hover | `0 10–12px 30–36px rgba(24,68,42,0.09–0.1)` |
| Button hover | `0 8–12px 24–32px rgba(24,68,42,0.22–0.25)` |
| Platform mockup | `0 24px 64px rgba(24,68,42,0.12), 0 4px 16px rgba(0,0,0,0.06)` |
| Floating stat card | `0 4–6px 24–28px rgba(0,0,0,0.09–0.14)` |

---

## Map (Hero)

- Library: **Leaflet.js** (`leaflet` npm package)
- Tiles: **CartoDB Positron** — `https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png`
- Center: `[25, 108]`, zoom: `4`
- All interactions disabled (pure visual)
- Trade routes: dashed polylines (`dashArray: '8 5'`)
  - Primary: `#18442A`, weight 2.5 — Shanghai → Hanoi
  - Secondary: `#45644A`, weight 1.8 — Guangzhou → HCMC
- City labels: custom `.map-label` tooltip, Montserrat 10px, white bg, forest border
- Markers: `L.divIcon` with pulsing CSS animation

---

## Animations

Keep motion **subtle only**:

| Pattern | Usage |
|---|---|
| `translateY(-2–4px)` on hover | Cards, buttons |
| `transition: 0.2s` | Card/button hover states |
| `transition: 0.35s ease` | Navbar state changes |
| `stroke-dashoffset` loop | Map trade route dashes |
| Pulse ring (scale + opacity) | Map city markers |
| Scroll-down line (scaleY) | Hero scroll indicator |

No entrance animations, no scroll-triggered effects — let content speak for itself.

---

## File Structure

```
src/
  layouts/
    Layout.astro        # HTML shell, global CSS vars, Google Fonts
  components/
    Navbar.astro        # Fixed nav, transparent→forest on scroll
    Hero.astro          # Full-viewport Leaflet map + content overlay
    About.astro         # Brand statement, 2 value blocks
    Solutions.astro     # Gom Gom platform, 4 pillars
    FinalCTA.astro      # Minimal centered CTA
    Footer.astro        # Dark footer, 3-column links
  pages/
    index.astro         # Assembles all components
public/
  logo.svg              # Full brand lockup, fills: #F3EDE3 (off-white)
  favicon.svg
```

---

## Design Principles (from brief)

1. **Minimal** — no decorative clutter, let whitespace breathe
2. **Premium** — generous padding, strong type hierarchy, subtle shadows
3. **B2B / High-trust** — no playful colors or gimmicks, strategic tone
4. **Strong typography** — headlines do the heavy lifting
5. **Subtle motion only** — hover states and map animations; no scroll fireworks
6. **Consistent surfaces** — always pick from the alternating bg pattern above
