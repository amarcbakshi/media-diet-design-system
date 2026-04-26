# DESIGN.md — Media Diet Design System

> Drop this file into any project or paste it into Claude Design during setup. It gives Claude everything needed to produce on-brand outputs without asking.

---

## Identity

**Project:** Media Diet  
**Website:** ourmediadiet.com  
**Tagline:** Step Inside America's Media Landscape  
**Nature:** Immersive documentary installation — physically reconstructed American media rooms from across the political spectrum. Visitors walk through three rooms and experience how the same news stories play out in completely different information ecosystems.  
**Designed by:** Will Rhodes (willrhodes.blue), December 2025  
**Tone:** Documentary, confrontational, restrained. Not "arts nonprofit." Not tech. Not editorial magazine.  
**References:** Forensic Architecture, Walker Art Center, Errol Morris  
**Anti-references:** Electric blue glow, tech product landing pages, arts nonprofit teal, Kickstarter documentary feel, anything that looks like it's trying to look designed

---

## Color System

Three colors only: **black, white, and cyan**.

| Name    | Hex       | CSS Token       | Use |
|---------|-----------|-----------------|-----|
| Black   | `#000000` | `--md-black`    | Primary backgrounds and surfaces |
| White   | `#FFFFFF` | `--md-white`    | Text, logos, outlines, button labels |
| Cyan    | `#00FFFF` | `--md-cyan`     | Highlight accent — use minimally |
| Gray 10 | `#1A1A1A` | `--md-gray-10`  | Subtle surface variation only |
| Gray 30 | `#4D4D4D` | `--md-gray-30`  | Secondary/metadata text |
| Gray 60 | `#999999` | `--md-gray-60`  | Tertiary text, placeholders |
| Gray 90 | `#E5E5E5` | `--md-gray-90`  | Hairline dividers on white |

### Cyan Rules — Strictly Observed
- Used **minimally**. Default to black and white; reach for cyan only when emphasis is genuinely needed.
- Appears **only on black or photographic backgrounds**. **Never on white.**
- Use for: stat callouts, subhead differentiation, a single focal accent per layout.
- Use for text or outlines only — **not as a fill**.

### Background Logic
- Default: **black background, white text**.
- Light pages: white background, black text — no cyan allowed.
- Photography: always full-bleed, carries all the color.

---

## Typography

**Typeface:** Suisse Int'l (Swiss Typefaces)  
Font files are in `/fonts/` — `SuisseIntl-Bold.otf` and `SuisseIntl-Medium.otf`.

| Role | Weight | File |
|------|--------|------|
| Headlines, taglines, promotional display | **Bold (700)** | `SuisseIntl-Bold.otf` |
| Body copy, UI, formal documents, subheads | **Medium (500)** | `SuisseIntl-Medium.otf` |

**Do not use Suisse Int'l Black for UI text.** Black weight is the wordmark's territory only.  
**Fallback stack:** `'Helvetica Neue', Arial, sans-serif`

### Type Scale
```
Hero display:   clamp(48px, 8vw, 120px)  — full-bleed lockup
H1:             clamp(32px, 5vw, 72px)   — section headers
H2:             clamp(24px, 3vw, 48px)   — subsection headers
H3:             20px                      — card titles
Body:           16px
Caption:        13px                      — metadata, footnotes
Label:          11px                      — button labels, tags
```

### Type Rules
- **All headlines: ALL CAPS.** Letter-spacing `0.02em–0.06em`. Bold weight.
- **Body: sentence case.** Medium weight. Max line length: 65ch.
- **Subheads:** Medium weight, differentiated from body via cyan color or increased spacing — not a different typeface.
- **Button labels:** ALL CAPS, 11px, letter-spacing `0.10em`.
- **No italic.** Use color (cyan) or spacing for emphasis, not style variants.
- **Line heights:** Display `1.0`, body `1.55`, caption `1.4`.

---

## Logo System

Two primary variants. Files in `/logos/`. **Do not alter letterforms or proportions.**

### Normal / Solid Variant
- Files: `logo-normal-white.svg` (on dark) / `logo-normal-black.svg` (on white)
- Extremely condensed heavy grotesque wordmark. "MEDIA DIET" stacked, all caps, full-width. Architectural and blunt.
- **Use over the brand's glass-effect imagery** (Paper app shader-processed photographs).

### Glass Variant  
- Files: `logo-glass-white.svg` / `logo-glass-black.svg`
- Same letterforms rendered as refractive/transparent outlines — ghostly, layered, as if made of material that bends light.
- **Use over normal (unprocessed) documentary photographs.**

### Pairing Logic
| Logo | Background |
|------|-----------|
| Normal (solid) | Glass-effect / shader-processed photography |
| Glass (refractive) | Normal documentary photography |
| Normal white | Flat black background |
| Normal black | Flat white background |

### The Glass Effect
A specific image treatment created using [Paper](https://paper.design) with custom shader parameters. Makes photography appear seen through refractive material. This is a **brand photography treatment only** — do not attempt to replicate with CSS `blur()`, `backdrop-filter`, or similar. Glass imagery is in `/images/glass/`.

### Glitch / Distorted Variant
Scan-line fragmentation effect. For editorial and social contexts only. **This treatment belongs to the logo exclusively** — never apply to UI elements, body text, or layout.

---

## Photography

**The rooms are the subject.** Documentary interiors: real American living rooms, dens, kitchens. TVs, bookshelves, personal objects. Warm, intimate, calm.

- **Always full-bleed** or edge-to-edge. Never in a box or card.
- **No rounded corners.** No drop shadows. No image borders.
- **No stock photography.** No people posing for camera.
- Images in `/images/glass/` show the brand's glass-effect treatment — use as hero/background imagery.
- Text over photography: white text + `linear-gradient(to top, rgba(0,0,0,0.85) 0%, rgba(0,0,0,0) 60%)` overlay. No frosted glass. No blur.
- Aspect ratios: hero — 16:9 or wider. Cards — 3:2.

---

## Components

### Buttons / CTAs
White outline box, no fill, uppercase label, 1.5px border. **This is the only button treatment.**

```css
.md-button {
  border: 1.5px solid currentColor;
  padding: 12px 24px;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.10em;
  text-transform: uppercase;
  color: #FFFFFF;
  background: transparent;
}
.md-button:hover {
  background: #FFFFFF;
  color: #000000;
}
```

No rounded corners. No shadows. No filled buttons. No gradients.

### Navigation
Flat. No backgrounds. No blur. Logo left, links right. All caps, 11px labels.  
On scroll: solid black bar only — no semi-transparent treatment.

### Form Fields
Underline border only (`border-bottom: 1px solid`). Transparent background. No box around fields.

### Stats / Callout Figures
Large number in cyan (`--md-cyan`), uppercase label in white below. Blunt. No decoration.

### Dividers
Hairline only (`1px solid rgba(255,255,255,0.15)` on dark; `rgba(0,0,0,0.12)` on light).

### Cards / Panels
No drop shadows. No rounded corners. Black or white backgrounds only — no grays as card surfaces. Use photography or 1px borders as visual elements.

---

## Spacing

```
4 / 8 / 16 / 24 / 32 / 48 / 64 / 96 / 128 / 192px
```

Grid: 12-column. Gutters: 32px. Margins: 48px minimum.  
Section rhythm: 128px–192px between major sections. **Generous space is intentional** — it amplifies the confrontational quality of the content.

---

## Motion

- Transitions: `0.15s–0.25s ease` on hover states and opacity fades only.
- No scroll-triggered animations. No elements flying in.
- No parallax.
- Video: autoplay muted, looped, full-bleed. Controls hidden until user-initiated.

---

## Voice & Copy

- **Direct and declarative.** One statement at a time.
- **No hedging.** "Most people never see how different someone else's information environment looks" — not "Many people may not always have the opportunity to…"
- **Statistics as blunt instruments.** Break the stat onto its own line. Let it land.
- **No clever wordplay** on the media diet metaphor — it's established once, not repeated.
- **Headline register:** ALL CAPS. Short. No punctuation except em-dashes.

---

## Do Not
- Use accent colors beyond cyan
- Use cyan on white backgrounds
- Apply rounded corners to images or containers
- Add drop shadows or depth effects
- Use the glitch effect anywhere outside the logo
- Use humanist serif or soft typefaces (no Garamond, Freight, Georgia)
- Use stock photography or staged/posed images
- Add frosted glass nav bars or backdrop-filter effects
- Add scroll-triggered reveals, parallax, or animated counters
- Make anything look like it's trying to look designed

---

## File Index

```
/DESIGN.md                    ← this file (primary Claude Design reference)
/logos/
  logo-normal-white.svg       ← solid wordmark on dark/glass-effect backgrounds
  logo-normal-black.svg       ← solid wordmark on white backgrounds
  logo-glass-white.svg        ← glass variant on normal photography (light logo)
  logo-glass-black.svg        ← glass variant on normal photography (dark logo)
/images/glass/                ← brand photography with glass-effect shader treatment
  cafe_under20mp.jpeg
  cameramen_under20mp.jpeg
  conversation_under20mp.jpeg
  crowd_under20mp.jpeg
  den_under20mp.jpeg
  family_under20mp.jpeg
  ... (26 images total)
/tokens/
  colors.css                  ← CSS custom properties for color
  typography.css              ← font declarations and type scale tokens
  spacing.css                 ← spacing scale, motion, border tokens
/components/
  components.css              ← buttons, nav, forms, stats, dividers
/fonts/
  SuisseIntl-Bold.otf         ← display / headlines (add manually — licensed)
  SuisseIntl-Medium.otf       ← body / UI (add manually — licensed)
```

---

*Brand design: Will Rhodes, December 2025 · Project: Amar C. Bakshi & Heidi Boisvert · ourmediadiet.com*
