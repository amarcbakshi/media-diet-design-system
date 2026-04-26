# DESIGN.md — Media Diet Design System

> Primary reference for Claude Design. Drop into any project or paste during Claude Design setup. All values sourced directly from the live website codebase (`media-diet-website`, Lucas Drummond).

**Site:** ourmediadiet.org · **Stack:** Nuxt 3 / SCSS · **Brand design:** Will Rhodes, Dec 2025

---

## Identity

**Project:** Media Diet  
**Tagline:** Step Inside America's Media Landscape  
**Nature:** Immersive documentary installation — physically reconstructed American media rooms from across the political spectrum. Visitors walk through three rooms and experience how the same news stories play out in completely different information ecosystems.  
**Tone:** Documentary, confrontational, restrained. Not arts nonprofit. Not tech. Not editorial magazine.  
**References:** Forensic Architecture, Walker Art Center, Errol Morris  
**Anti-references:** Electric blue glow, tech product landing pages, arts nonprofit teal, anything trying to look designed

---

## Color System

Sourced from `app/assets/styles/_vars.scss`.

| Name | Hex | SCSS Variable | Use |
|------|-----|---------------|-----|
| Off-black | `#141414` | `$color-offblack` | **Site background** — primary surface |
| Off-white | `#F0F1F4` | `$color-offwhite` | **Site text** — primary text color |
| Cyan | `#00FFFF` | `$color-cyan` | Accent — use minimally |
| Cyan dark | `#01BBBB` | `$color-cyan-dark` | Focus outlines, interactive accents |
| Tan | `#E8E1D4` | `$color-tan` | Warm secondary surface |
| Dark grey | `#313131` | `$color-darkgrey` | Elevated surfaces |
| Grey | `#666666` | `$color-grey` | Secondary/metadata text |
| Light grey | `#C4C4C4` | `$color-lightgrey` | Tertiary text, disabled states |
| White | `#FFFFFF` | `$color-white` | High-contrast contexts only |
| Error | `rgb(162,0,0)` | `$color-error` | Errors only |
| Border light | `rgba(0,0,0,0.12)` | `$color-border-light` | Dividers on light backgrounds |
| Border dark | `rgba(240,241,244,0.15)` | `$color-border-dark` | Dividers on dark backgrounds |

**Stance colors** (used in content analysis UI only — not general brand):
- Left: `#4A90D9` · Right: `#D94A4A` · Center: `#666666`

### Color Rules
- **Default:** `#141414` background, `#F0F1F4` text. Not pure black/white.
- **Cyan** (`#00FFFF`) is a highlight only — minimal use, on dark/photographic backgrounds, never on the tan or white backgrounds.
- **Cyan dark** (`#01BBBB`) is used for focus outlines (`$site-outline-color`) and interactive states.
- `$color-tan` (`#E8E1D4`) appears in warmer content sections and secondary surfaces.

---

## Typography

Sourced from `app/assets/styles/typography.scss` and `_vars.scss`.

**Typeface:** Suisse Int'l  
Font served from `/public/fonts/suisse/`. In CSS: `font-family: "Suisse"`.  
Fallbacks: `"Bricolage Grotesque"` (display) · `"Helvetica Neue"`, `"Helvetica"`, `sans-serif`

```scss
$font-display: "Suisse", "Bricolage Grotesque", "Helvetica Neue", "Helvetica", sans-serif;
$font-body:    "Suisse", "Helvetica Neue", "Helvetica", sans-serif;

$weight-black:   900;
$weight-bold:    700;
$weight-medium:  500;
$weight-regular: 400;
$weight-light:   300;
$weight-thin:    100;
```

### Type Scale (responsive — mobile / tablet / desktop)

| Element | Size | Weight | Case | Line Height |
|---------|------|--------|------|-------------|
| `h1` | 50 / 70 / 80px | Bold (700) | Mixed | 0.95em |
| `h2` | 38 / 52 / 60px | Medium (500) | Mixed | 0.90em |
| `h3` | 29 / 35 / 40px | Medium (500) | Mixed | 1.00em |
| `h4` | 20 / 25 / 30px | Medium (500) | Mixed | 1.00em |
| `h5` | 12 / 14 / 16px | Bold (700) | **UPPERCASE** | 1.00em |
| `.subtitle` | 10 / 11px | Bold (700) | **UPPERCASE** | — |
| `.p--extra-large` | 20 / 22 / 24px | Regular | Mixed | 1.3em |
| `.p--large` | 17 / 18 / 19px | Regular | Mixed | 1.3em |
| `p` / `.p--regular` | 14 / 15 / 16px | Regular | Mixed | 1.3em |
| `.p--small` | 11 / 13 / 14px | Regular | Mixed | 1.3em |

**Subtitle** additionally has: `text-decoration: underline`, `text-underline-offset: 4px`, `letter-spacing: 0.06em`.

**Note:** H1–H4 are **mixed case**, not all caps. All-caps is reserved for `h5`, `.subtitle`, and the logo wordmark treatment only.

---

## Logo System

Two primary variants. Files in `/logos/`. Do not alter letterforms or proportions.

### Normal / Solid Variant
- `logo-normal-white.svg` · `logo-normal-black.svg`
- Extremely condensed heavy grotesque wordmark. "MEDIA DIET" stacked, all caps.
- **Use over glass-effect imagery** (Paper app shader-processed photos).
- On dark flat backgrounds: white variant. On light flat backgrounds: black variant.

### Glass Variant
- `logo-glass-white.svg` · `logo-glass-black.svg`
- Same letterforms as refractive/transparent outlines — ghostly, layered.
- **Use over normal (unprocessed) documentary photographs.**

### Pairing Logic
| Logo | Background |
|------|-----------|
| Normal (solid) | Glass-effect / shader-processed photography |
| Glass (refractive) | Normal documentary photography |
| Normal white | Flat dark (`#141414`) background |
| Normal black | Flat light background |

### The Glass Effect
A specific image treatment created using [Paper](https://paper.design) with custom shader parameters. **This is a photography treatment only** — do not replicate with CSS `blur()` or `backdrop-filter`. Glass imagery lives in `/images/glass/`.

### Glitch / Distorted Variant
Scan-line fragmentation. Editorial and social only. **Never apply to UI elements or layout.**

---

## Grid & Layout

Sourced from `_vars.scss` and `main.scss`.

```scss
// Columns
Mobile:  12 columns, 16px gutters, 8px side padding
Tablet:  18 columns, 18px gutters, 12px side padding
Desktop: 24 columns, 18px gutters, 24px side padding

// Section padding
Mobile:  48px top/bottom, 8px sides
Tablet:  72px top/bottom, 12px sides
Desktop: 96px top/bottom, 24px sides

// Section height
Mobile:  calc(110vh + 50px)
Tablet:  calc(105vh + 55px)
Desktop: calc(100vh + 60px)

// Header height
Mobile: 50px · Tablet: 55px · Desktop: 60px
```

---

## Spacing

```scss
$margin-extra-large: 48px;
$margin-large:       32px;
$margin-normal:      24px;
$margin-small:       12px;
$margin-extra-small:  6px;
```

Utility classes: `.mb-0` `.mb-half` `.mb-1` `.mb-2` `.mb-3` `.mb-4` (and `mt-*` equivalents).

---

## Border Radius

```scss
$border-radius-small:  8px;
$border-radius-medium: 12px;
$border-radius-large:  16px;
```

Rounded corners **are used** on interactive elements, cards, and form fields. Photography is always sharp (no border-radius on images).

---

## Motion & Easing

Sourced from `_vars.scss`.

```scss
// Speeds
$speed-demon:  333ms;   // Fast interactions
$speed-metal:  666ms;   // Standard transitions
$speed-danger: 1000ms;  // Slow/deliberate

// Named easings
$evil-ease:          cubic-bezier(0.666, 0, 0.333, 1);
$steezy-ease:        cubic-bezier(0.85, 0, 0.15, 1);
$ease-out:           cubic-bezier(0, 0, 0.666, 1);
$ease-out-cubic:     cubic-bezier(0.33, 1, 0.68, 1);
$ease-out-quint:     cubic-bezier(0.22, 1, 0.36, 1);
$ease-in-out:        cubic-bezier(0.65, 0, 0.35, 1);
$ease-in-out-quint:  cubic-bezier(0.83, 0, 0.17, 1);
$bouncy:             cubic-bezier(0, 0.888, 0.333, 1.222);
$ease-out-back:      cubic-bezier(0.34, 1.56, 0.64, 1);
```

Page transitions: `opacity` fade at `$speed-metal`. Swap transitions: `opacity` + `scale(0.3)` at `$speed-demon` with `$bouncy` easing. Images: `opacity 0 → 1` at `666ms ease` on lazy load.

---

## Components

### Buttons
```scss
button {
  color: $color-offwhite;
  outline-color: $site-outline-color; // #01BBBB
  background-color: transparent;
  border: none;
}
```
The site uses custom button components with background images (`button-bg-dark.png`, `button-bg-light.png`, `button-bg.svg` in `/public/`). Always outline style; never solid fill.

### Links
```scss
a {
  color: $color-offwhite;
  text-decoration: none;
  outline-color: $color-cyan-dark; // #01BBBB
  &:hover { font-weight: $weight-bold; }
}
```

### Form Fields
```scss
$form-field-color:            $color-offblack;
$form-field-background-color: transparent;
$form-field-border:           2px solid $color-offblack;
$form-field-placeholder-color: $color-grey;
$form-field-focus-color:      $color-offwhite;
```

### Photography
- Always full-bleed. No rounded corners on images.
- Lazy loaded: `opacity: 0` → `opacity: 1` at `666ms ease`.
- Text overlays: `linear-gradient(transparent, rgba(0,0,0,1))` via `.under-shadow` utility.

### Border Frame
Decorative inset border treatment (`.border-frame`) using `::before`/`::after` pseudo-elements with `1px solid currentColor` offset by `$margin-small` (12px) on all sides.

---

## Media Queries

```scss
$large-mobile:    "(min-width: 500px)";
$tablet:          "(min-width: 768px)";
$large-tablet:    "(min-width: 960px)";
$desktop:         "(min-width: 1280px)";
$average-desktop: "(min-width: 1440px)";
$macbook:         "(min-width: 1680px)";
$retina-macbook:  "(min-width: 1920px)";
$largest-screens: "(min-width: 2000px)";
```

Usage: `@include respond-to($tablet) { ... }`

---

## Photography

**The rooms are the subject.** Warm, intimate, calm. Domestic interiors — real American living rooms, dens, kitchens. TVs, bookshelves, personal objects.

- Full-bleed. No rounded corners. No shadows on images.
- No stock photography. No staged/posed images.
- Glass-effect images (in `/images/glass/`) use the Paper app shader treatment.
- Normal portrait photography of creators: `amar-portrait.webp`, `heidi-portrait.jpeg` (available in site `/public/`).

---

## Voice & Copy

- Direct and declarative. One statement at a time.
- No hedging. No clever riffs on the "media diet" metaphor — established once, not repeated.
- Statistics land alone: break numbers onto their own line.
- Headline register: concise, no punctuation except em-dashes.
- H5 / subtitle labels are uppercase; H1–H4 headings are mixed case.

---

## File Index

```
/DESIGN.md                     ← this file
/logos/
  logo-normal-white.svg        ← solid wordmark, use over glass-effect imagery
  logo-normal-black.svg        ← solid wordmark, use on light backgrounds
  logo-glass-white.svg         ← glass variant, use over normal photography
  logo-glass-black.svg         ← glass variant, use over normal photography
/images/glass/                 ← 26 brand photos with glass-effect shader treatment
/fonts/
  SuisseIntl-Bold.otf          ← display weight (700)
  SuisseIntl-Medium.otf        ← body/UI weight (500)
/tokens/
  colors.css                   ← CSS custom properties
  typography.css               ← font declarations and scale
  spacing.css                  ← spacing, motion, borders
/components/
  components.css               ← buttons, nav, forms, stats, dividers
```

---

*Brand design: Will Rhodes (willrhodes.blue) · Web: Lucas Drummond · Project: Amar C. Bakshi & Heidi Boisvert · ourmediadiet.org*
