# Prospectra — Brand Style Guide

The applied rules for the Prospectra identity. Locked spec lives in the brain repo
(`decisions/D-02_brand_identity.md`, `PROJECT_FOUNDATION.md §8`); this file is the
operator's reference for using the kit. Positioning is **editorial publication, not
software platform** — warm, considered, type-forward.

- **Brand name:** Prospectra ("Geospatial" is a contextual descriptor, never part of the mark)
- **Tagline:** *Geospatial analytics, indexed to the cell.*
- **Manifesto:** *Every business problem has a location. Most companies leave that signal on the floor. We pick it up, give it an address, and put it to work.*

---

## 1. Logo

The mark is a **7-hex H3 cluster** — one central cell surrounded by six. The centre cell
is filled terracotta; the six children are outlined. It reads, to anyone with H3
experience, as a parent cell with its res+1 children. That literal reading is the point —
do not stylise it away.

### Files in this kit

| File | What it is | Use for |
|---|---|---|
| `prospectra-mark.svg` | Mark, ink outline + terracotta centre, transparent | Default mark. Navbar, favicons-from-source, anywhere on paper/light. |
| `prospectra-mark-mono.svg` | Mark, single-colour ink (centre also ink) | One-colour contexts: stamps, watermarks, print where terracotta can't render. |
| `prospectra-mark-reversed.svg` | Mark on ink `#19150f` block, terracotta centre | Dark backgrounds — X title cards, dark sections. |
| `prospectra-wordmark.svg` | "prospectra" lowercase + terracotta dot, no mark | Tight horizontal space where the mark would be too small to read. |
| `prospectra-lockup.svg` | Mark + wordmark + terracotta dot separator | Primary horizontal lockup. Banners, headers, social. |
| `prospectra-lockup-mono.svg` | Lockup, single-colour ink | One-colour horizontal contexts. |
| `prospectra-mark.png` | 1024² raster of the mark | Raster fallback. **Note: white background, not transparent** — fine on white, not on cream. Prefer the SVG. |
| `prospectra-mark-favicon-512.png` | 512² mark on cream | High-res raster on brand surface (OG fallback, app tiles). |

### Rules

- **Minimum size:** mark no smaller than **24 px** on screen (below that the outlined
  hexes collapse — use the favicon set instead). Lockup no smaller than **120 px** wide.
- **Clear space:** keep padding around the mark of at least the width of one outer hex
  (≈ ¼ of the mark's width). Don't crowd it with text or rules.
- **Wordmark is always lowercase** — "prospectra", never "Prospectra" or "PROSPECTRA"
  in the logotype. (Sentence-case "Prospectra" is correct in running prose.)
- **The terracotta dot** (·) after the wordmark is part of the lockup. Don't drop it,
  don't recolour it.
- **Don't:** recolour the mark outside the palette, add gradients/shadows, rotate it,
  stretch it non-uniformly, or place the standard (non-reversed) mark on a dark or busy
  background — switch to the reversed or mono variant instead.

---

## 2. Palette

Tokens live in `palette.json` and `palette.scss` (keep them in sync). Hex values are
canonical in `PROJECT_FOUNDATION.md §8`.

| Token | Hex | Role |
|---|---|---|
| `paper` | `#f3eee5` | Primary surface. The default background everywhere. |
| `paper-soft` | `#ebe5da` | Secondary surface — status banners, cards, callouts. |
| `paper-deep` | `#e0d9cb` | Tertiary surface — insets, footer, code-block backgrounds. |
| `ink` | `#19150f` | Body text + headings. Deep warm brown-black, **never pure `#000`**. |
| `ink-soft` | `#2a241c` | Softened body text where full ink is too heavy. |
| `muted` | `#756a59` | Metadata, captions, eyebrows, secondary copy. |
| `hair` | `#d4cbb9` | Hairline borders and rules (1px). |
| `accent` | `#b8421a` | Terracotta. Links, active hexes, project codes, the dot. |
| `accent-deep` | `#8f2f0f` | Accent hover / pressed / visited. |

### Usage discipline

- **Accent is a pop, not a fill.** Terracotta marks one or two things per view — a link,
  an active hex, a "shipping" status. If half the page is terracotta, it stops meaning
  anything. Large warm areas should be `paper-soft` / `paper-deep`, not accent.
- **Muted carries all the editorial furniture** — coordinates, eyebrows, dates, captions.
  Body prose is `ink`; everything that supports it is `muted`.
- **Hairlines, not boxes.** Separate sections with a `hair` rule, not heavy borders or
  drop-shadowed cards.
- The palette is deliberately warm. **Don't introduce a cool secondary** (blue/teal)
  without a deliberate decision — it fights the earthenware tone (see D-02 trade-offs).

---

## 3. Typography

| Role | Typeface | Notes |
|---|---|---|
| Display | **Fraunces** (variable serif, optical sizing) | Headlines, hero, manifesto, section heads. Light/regular weight, tight tracking (`-0.02em`). Never for body. |
| Body / UI | **DM Sans** (geometric sans) | All running copy, nav, buttons. |
| Mono / meta | **IBM Plex Mono** | Code, coordinates, eyebrows, project codes (`P-01`), ticker stats, dates. |

- **Fraunces is display only.** It earns its keep at large sizes where the optical axis
  shows. Don't set paragraphs in it.
- **Eyebrows** are uppercase IBM Plex Mono, `muted`, with generous letter-spacing
  (`0.16em`), usually above a `hair` rule.
- **Project codes** (`P-01`, `L-05`) are IBM Plex Mono, `accent`, uppercase.
- Fonts load from Google Fonts in `custom.scss`. Keep the variable-font axes there so
  the payload stays in one place.

---

## 4. Signature visual elements

### a. Hex-grid background

A faint honeycomb with a few "active" terracotta cells. Use behind heroes and section
breaks at low opacity — it should whisper, not shout. Reduce opacity if it competes with
text. Reusable snippet (tune `stroke`, `opacity`, and active-cell positions per use):

```html
<div class="hex-bg" aria-hidden="true">
  <svg viewBox="0 0 1400 900" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMidYMid slice">
    <defs>
      <pattern id="hexpat" width="60" height="52" patternUnits="userSpaceOnUse">
        <polygon points="15,0 45,0 60,26 45,52 15,52 0,26"
                 fill="none" stroke="#19150f" stroke-width="0.8"/>
      </pattern>
    </defs>
    <rect width="100%" height="100%" fill="url(#hexpat)"/>
    <!-- a few active hexes — terracotta, varying opacity -->
    <polygon points="375,260 405,260 420,286 405,312 375,312 360,286" fill="#b8421a"/>
    <polygon points="555,468 585,468 600,494 585,520 555,520 540,494" fill="#b8421a" opacity="0.6"/>
    <polygon points="975,156 1005,156 1020,182 1005,208 975,208 960,182" fill="#b8421a" opacity="0.4"/>
    <polygon points="855,624 885,624 900,650 885,676 855,676 840,650" fill="#19150f" opacity="0.5"/>
  </svg>
</div>
```

```css
.hex-bg { position: absolute; inset: 0; z-index: 0; opacity: 0.10; pointer-events: none; }
.hex-bg svg { width: 100%; height: 100%; }
```

A single hexagon (for ticker rows, list bullets, card corners):
`points="15,0 45,0 60,26 45,52 15,52 0,26"` in a 60×52 box.

### b. LAT/LON corner detail

Editorial coordinates as a corner flourish — Madrid's coordinates by default. IBM Plex
Mono, `muted`, small. Top-right of a hero or footer corner.

```html
<div class="coords">
  <div>LAT <span>40°25′ N</span></div>
  <div>LON <span>3°42′ W</span></div>
</div>
```

```css
.coords { font-family: "IBM Plex Mono", monospace; font-size: 0.8rem;
          color: #756a59; line-height: 1.5; text-align: right; }
.coords span { color: #19150f; }
```

Use real coordinates tied to the content where it makes sense (a project's study area);
otherwise Madrid `40°25′ N · 3°42′ W` is the house default.

---

## 5. Favicons

Generated from the mark's vector geometry onto a `paper` (`#f3eee5`) ground —
not from `prospectra-mark.png` (which has a white background).

- `favicon.ico` — multi-resolution (16 / 32 / 48), referenced in `_quarto.yml`
- `favicon-16x16.png`, `favicon-32x32.png` — explicit sizes
- `apple-touch-icon.png` — 180², flattened (no alpha)

At 16 px the six outer hexes go faint and the terracotta centre carries the mark — this
is expected. If a tighter 16 px glyph is wanted, simplify to the central filled hex only
(tracked as T14 in the build plan).

---

## 6. Links

- Editable Figma source (X title card, LinkedIn banner, OG image templates): _TODO — paste
  link after T12/T13/T14._
- Brand decision record: `decisions/D-02_brand_identity.md` (brain repo)
- Live brand record: `PROJECT_FOUNDATION.md §8` (brain repo)
