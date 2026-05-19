# Vantia — Brand Assets

> Status: **v1 LOCKED** 2026-05-18 · Tokens (Phase C1) + Wordmark (Phase C2) approved · Phase D live.
> Canonical domain: **`vantia.pro`** (2026-05-18). Optional defensive: `vantia.cloud`.

## What's in here

```
brand-assets/vantia/
├── README.md                  ← this file
├── tokens-proposal.md         ← LOCKED design tokens (colors, type, spacing, etc.)
├── wordmark-light.svg         ← VANTIA wordmark for light surfaces (navy #061b31)
├── wordmark-dark.svg          ← VANTIA wordmark for dark surfaces (lime #a9d13c)
├── wordmark-mono.svg          ← VANTIA monochrome for print/fax/single-colour
├── web/
│   └── favicon-mark.svg       ← Single "V" mark for ≤32px contexts (tab favicon, app icon)
├── documents/                 ← (PNGs pending — see "Rendering PNGs" below)
├── email/                     ← (PNGs pending)
└── social/                    ← (PNGs pending)
```

## Wordmark spec

| Aspect | Value |
|---|---|
| Letterform | `vantia.` — lowercase + **trailing lime brand circle** (β 1.2×, tight) |
| Font family | Söhne (master) → SF Pro Display → Helvetica Neue → system-ui (fallback) |
| Weight | 400 (regular) on all variants — robust to font fallback |
| Letter-spacing | -3px at 120px size (~ -0.025em tight, "precise" feel) |
| Light variant | navy `#061b31` letters + lime `#a9d13c` circle |
| Dark variant | white `#ffffff` letters + lime `#a9d13c` circle |
| Mono variant | black `#000000` (circle inclusive) — print/fax/single-colour |
| Circle | filled disc, ~1.2× the equivalent period glyph width, tight against the "a", raised slightly above baseline (visual centre above x-height) |
| Aspect ratio | 3:1 (viewBox 600×200) — square-ish, fits header bands and slide titles well |
| Favicon mark aspect | 1:1 (viewBox 64×64) — navy square with white `v` + lime circle |

**Why Option 2 (vs Option 3 UPPERCASE TRACKED):** Option 3 depended critically on Söhne being installed — at light weight + wide tracking, font fallback noticeably degrades. Option 2 is resilient: lowercase + regular weight + dot-as-signature renders consistently across SF Pro, system-ui, DejaVu Sans, and any reasonable fallback. The brand colour (lime dot) carries the identity regardless of which font shows.

## When to use which

| Context | File | Why |
|---|---|---|
| Light hero, web header, doc header | `wordmark-light.svg` | Navy on light surfaces — primary brand mark |
| Dark hero, slides with dark theme, video bumper | `wordmark-dark.svg` | Lime on dark — brand colour brilha |
| B&W print, fax, single-colour merchandise | `wordmark-mono.svg` | Weight 400 (regular) for print legibility |
| Browser tab, PWA app icon, OS taskbar | `web/favicon-mark.svg` | Full wordmark `vantia.` compressed at ≤32px — favicon shows `v.` (white v + lime dot) on navy rounded square, preserving the dot signature |
| Profile pictures (Twitter/X, GitHub org, etc.) | `web/favicon-mark.svg` | Same as favicon — square avatar works |

## Rendering PNGs

The SVG masters are the source of truth. For rasterized PNG variants (per the pattern used in `brand-assets/ritmo/`), use either:

**Option A — browser screenshot:** open the SVG in Chrome/Safari, zoom to desired size, screenshot. Crude but works.

**Option B — automated via headless chromium** (already on host at `/opt/chromium-playwright/chrome-linux64/chrome`):
```bash
chromium --headless --no-sandbox --disable-gpu \
  --screenshot=/path/to/out.png --window-size=600,200 \
  file:///root/nanoclaw/groups/global/brand-assets/vantia/wordmark-light.svg
```

**Option C — proper export via design tool** (Figma, Illustrator) when commissioning the final Söhne font.

**Recommended dimensions** (per Ritmo brand-kit-guide):
- Email header: 200×67 (light + dark)
- Email retina: 400×134 (light + dark)
- Document header: 300×100 + 600×200 (alta resolução)
- Presentation slides: 250×83
- Social posts: 400×134
- Web hero: 200×67 + 300×100
- Favicon: 32×32, 64×64, 192×192 (from `favicon-mark.svg`)

## Known limitations of v1

1. **Söhne not licensed** — without the actual Söhne font installed, browsers render the SF Pro Display fallback. Visual fidelity ~85% of intent. Resolve by either (a) commissioning Söhne, (b) converting text to outlines in a design tool when fixing the master, or (c) accepting the fallback as canonical (legitimate choice — many studios run on system fonts).

2. **PNG renders not bundled** — only SVG masters exist. Generate PNGs as needed via Option B above.

3. **No social asset templates** — Vantia OG images, Twitter cards, LinkedIn banners not yet produced. Phase D may include templates that Open Design daemon can generate on demand via skills.

4. **No animated logo** — no motion lockup. Probably not needed for Vantia identity but flagged for completeness.
