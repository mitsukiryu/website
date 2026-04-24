# DESIGN.md — Caffeine Tierlist Website

## 1. Design Philosophy

**Cyberpunk pixel art.** The site feels like a neon-lit arcade cabinet in a rainy Tokyo back alley. Pixel art sprites are the primary visual language — not decoration, but the main content. The dark background makes neon colors pop the way wet pavement reflects street signs. Target audience is students and developers: people who live on caffeine and appreciate retro-digital aesthetics.

Reference images:
- `pixelart_web_ex.png` — pixel art integration into web layout (sprite-as-hero, card grids)
- `neon_sign_kinda.jpg` — color mood, atmosphere (dark + layered neons)

---

## 2. Color Palette

| Role              | Name           | Hex       | Usage                                      |
|-------------------|----------------|-----------|--------------------------------------------|
| Background        | Void           | `#0a0a14` | Page background                            |
| Surface           | Dark Panel     | `#12121f` | Cards, panels, containers                  |
| Surface Raised    | Raised Panel   | `#1a1a2e` | Hover states, modals, dropdowns            |
| Border            | Dim Line       | `#2a2a40` | Dividers, card borders                     |
| Neon Cyan         | Cyber Cyan     | `#00f5ff` | Primary accent, S-tier, CTAs, links        |
| Neon Magenta      | Neon Pink      | `#ff00cc` | Secondary accent, highlights, badges       |
| Neon Amber        | Volt           | `#ffd600` | Warnings, A-tier, star ratings             |
| Neon Red          | Hot Red        | `#ff2244` | Danger states, D/F-tier labels             |
| Neon Green        | Matrix Green   | `#00ff41` | Success states, online indicators          |
| Text Primary      | Ghost White    | `#e8e8f0` | Body text, card titles                     |
| Text Secondary    | Dim Gray       | `#888899` | Subtitles, metadata, placeholders          |
| Text Disabled     | Dead Pixel     | `#444455` | Disabled elements                          |

### Neon Glow Effects
Neon-colored elements should use `box-shadow` or `text-shadow` to simulate the bloom effect from physical neon signs:
```css
/* Example: Cyan glow */
text-shadow: 0 0 8px #00f5ff, 0 0 20px #00f5ffaa;
box-shadow: 0 0 8px #00f5ff, 0 0 24px #00f5ff66;
```

---

## 3. Typography

### Font Choice
**Primary font**: `Press Start 2P` (Google Fonts)
- Authentic 8x8 pixel bitmap font, directly based on IBM's VGA character set
- Use for: headings, tier labels, navigation items, UI labels, buttons
- Load via: `https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap`

**Secondary font**: `VT323` (Google Fonts)
- Pixel-style monospace, more readable at small sizes than Press Start 2P
- Use for: body text, descriptions, card metadata, longer text blocks
- Load via: `https://fonts.googleapis.com/css2?family=VT323&display=swap`

### Type Scale

| Label        | Font           | Size    | Weight | Usage                         |
|--------------|----------------|---------|--------|-------------------------------|
| Display      | Press Start 2P | 32px    | 400    | Page hero title               |
| H1           | Press Start 2P | 24px    | 400    | Section headings              |
| H2           | Press Start 2P | 18px    | 400    | Card titles, tier labels      |
| H3           | Press Start 2P | 14px    | 400    | Sub-labels, nav items         |
| Body Large   | VT323          | 20px    | 400    | Primary body text             |
| Body         | VT323          | 18px    | 400    | Descriptions, metadata        |
| Small        | VT323          | 16px    | 400    | Tags, captions                |
| Micro        | Press Start 2P | 8px     | 400    | Badges, scores, corner labels |

> Note: Press Start 2P renders at effective sizes twice what you'd expect — 8px already looks large. Avoid using it below 8px.

### Line Height & Letter Spacing
- `Press Start 2P`: `line-height: 2` (the font needs extra breathing room)
- `VT323`: `line-height: 1.4`
- No additional `letter-spacing` needed — bitmap fonts are already spaced per-glyph

---

## 4. Spacing & Layout

### Base Unit
`8px` is the base spacing unit. All margins, paddings, and gaps should be multiples of 8.

| Token  | Value | Common use                        |
|--------|-------|-----------------------------------|
| `xs`   | 4px   | Icon padding, tight inline gaps   |
| `sm`   | 8px   | Inner padding on small elements   |
| `md`   | 16px  | Standard card padding             |
| `lg`   | 24px  | Section inner padding             |
| `xl`   | 32px  | Between sections                  |
| `2xl`  | 48px  | Page-level vertical rhythm        |
| `3xl`  | 64px  | Hero section spacing              |

### Grid
- **Page max-width**: 1280px, centered
- **Page horizontal padding**: 24px (mobile), 48px (desktop)
- **Column grid**: 12-column, `gap: 16px`
- **Card grid**: auto-fill, `minmax(240px, 1fr)`, `gap: 16px`

### Borders & Corners
- **Border radius**: `0px` — pixel art aesthetic demands sharp corners. No `border-radius`.
- **Border style**: `1px solid` using `Dim Line (#2a2a40)` by default; neon color border on hover/active
- **Pixel border alternative**: For key elements (tier rows, hero cards), use a 2px or 4px neon-colored border with matching glow

---

## 5. Visual Style Rules

### Pixel Art Integration
- Sprites render at exact integer scale only — `1x`, `2x`, `4x` (no fractional scaling)
- Use `image-rendering: pixelated` on all `<img>` tags displaying pixel art
- Minimum render size for sprites: `64x64px` displayed; recommended `128x128px` or `256x256px`
- Do not apply CSS filters (blur, drop-shadow) directly on pixel sprites — it destroys crispness

### Scanline Overlay (Optional Enhancement)
A subtle scanline effect can be applied as a full-screen overlay using a repeating CSS gradient to reinforce the CRT/arcade monitor feel. This is a `::before` pseudo-element on the root container — low opacity (5–10%) so it doesn't obscure content.

### Neon UI Elements
- Buttons: flat background with neon-colored border + text + glow on hover
- Active/selected states: filled neon background with dark text
- No gradients — keep colors flat and pixel-accurate

---

## 6. Tier Label Colors

Standard tier row colors for the tierlist feature:

| Tier | Color Name     | Hex       | Glow Color  |
|------|----------------|-----------|-------------|
| S    | Cyber Cyan     | `#00f5ff` | `#00f5ff`   |
| A    | Volt           | `#ffd600` | `#ffd600`   |
| B    | Neon Green     | `#00ff41` | `#00ff41`   |
| C    | Ghost White    | `#e8e8f0` | `#e8e8f0`   |
| D    | Neon Pink      | `#ff00cc` | `#ff00cc`   |
| F    | Hot Red        | `#ff2244` | `#ff2244`   |

---

## 7. Required Assets

> Assets must be provided externally. Do not auto-generate or substitute with placeholders in production.

### Pixel Art Sprites (Per Beverage)
Each beverage on the tierlist needs a dedicated pixel art sprite:
- **Format**: PNG with transparent background
- **Canvas size**: 64x64px (source), scaled up 4x to 256x256px in the UI
- **Style**: Consistent perspective (slight front-facing isometric or flat front view), consistent light source (top-left), consistent outline weight (1px dark outline)
- **Examples needed** (at minimum for V1):
  - Canned energy drink (generic — Red Bull style)
  - Coffee cup (paper cup with lid)
  - Espresso shot (small ceramic cup)
  - Green tea bottle
  - Cola can
  - Matcha latte cup

### UI Pixel Art Elements
- Site logo / wordmark in pixel art style
- Tier label decorations (optional: small pixel icons next to S/A/B etc.)
- Background tile or pattern (optional: pixel city skyline, or a subtle dark grid)

### Fonts
Both fonts are from Google Fonts — no download needed, loaded via CDN:
- `Press Start 2P`
- `VT323`

---

## 8. Accessibility Notes

- Neon on dark passes contrast for large text (Press Start 2P at 14px+) — verify with WCAG AA for body text sizes
- `VT323` body text at 18px on `#0a0a14` background with `#e8e8f0` color: contrast ratio ~14:1 (passes AAA)
- Avoid relying solely on color to convey tier ranking — pair color with the letter label
- Glow effects are purely decorative — no semantic meaning attached to them
