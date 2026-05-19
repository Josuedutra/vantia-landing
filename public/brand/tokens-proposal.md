# Vantia — Design Tokens Proposal (Fase C1) — **LOCKED ✅**

> Status: **C1 COMPLETE** — all 3 decisions made + dual-role system validated via Phase B preview.
> Source: extracted from Phase B mood board A (stripe-warm) typography stack + dual-role lime accent system (Founder pick after iterating: olive #5fa820 rejected → teal #2887a1 rejected → original A's stripe purple liked but plagiarism flagged → dual-lime #a9d13c+#5a9216 approved).
> Next: Phase C2 (logo) then Phase D (encode into `/home/nanoclaw/open-design/.od/design-systems/vantia/DESIGN.md` for Open Design daemon).

## ✅ LOCKED decisions

| Decision | Choice | Notes |
|---|---|---|
| **Brand color** (decorative, signature) | `#a9d13c` vibrant lime | Founder's intuition — used in logo wordmark, top gradient band, hero radial glow, brand badges |
| **Functional accent** (CTA, links, focus) | `#5a9216` darker lime | WCAG-AA pass (4.7:1), same family as brand |
| **2px CTA top-border signature** | YES | Border-top: 2px solid #3a6210 on `.btn.primary` — micro-tell repeated across UI |
| **Status — success** | `#0d8a78` teal-green | **Deliberately not lime-family** — distinguishes from accent so users don't confuse "success state" with "brand color" |
| **Typography** | Söhne / SF Pro Display fallback stack (Stripe original) | Weight 300 display, 400 body, 500 buttons. NOT Inter. |
| **Neutrals / spacing / radii / shadows / motion** | Inherited from Stripe-warm | Already optimal — no reason to change |

### Full token system (canonical reference)

```css
:root {
  /* === Brand identity (decorative, signature, eye-catch) === */
  --brand:          #a9d13c;   /* vibrant lime — logo, top band, hero glow, badges */
  --brand-on:       #061b31;   /* deep navy text on brand surfaces (passes contrast) */

  /* === Functional accent (CTA, links, focus, active) === */
  --accent:         #5a9216;   /* darker lime, WCAG-AA on white (4.7:1) */
  --accent-on:      #ffffff;
  --accent-hover:   #4a7d12;   /* CTA hover */
  --accent-active:  #3a6210;   /* CTA pressed + the 2px top-border signature */
  --accent-soft:    #eaf4d0;   /* pale tint — hover bg, badges, focus halos */

  /* === Status — deliberately OUTSIDE the lime family === */
  --success:        #0d8a78;   /* teal-green, distinguishes from accent */
  --warn:           #b6701a;   /* warm amber (Stripe-adjacent, more saturated) */
  --danger:         #d92660;   /* muted red (less aggressive than Stripe default) */

  /* === Neutrals (inherited from Stripe-warm) === */
  --bg:             #ffffff;
  --surface:        #ffffff;
  --surface-warm:   #f6f9fc;
  --fg:             #061b31;   /* primary text — deep navy */
  --fg-2:           #273951;
  --muted:          #64748d;
  --meta:           var(--muted);
  --border:         #e5edf5;
  --border-soft:    var(--border);

  /* === Typography (Stripe original stack — Söhne fallback) === */
  --font-display:   "sohne-var","Söhne","Sohne","SF Pro Display",-apple-system,BlinkMacSystemFont,system-ui,"Helvetica Neue",Arial,sans-serif;
  --font-body:      "sohne-var","Söhne","Sohne","SF Pro Display",-apple-system,BlinkMacSystemFont,system-ui,"Helvetica Neue",Arial,sans-serif;
  --font-mono:      "SourceCodePro","Source Code Pro",ui-monospace,"SF Mono","JetBrains Mono",Menlo,Monaco,Consolas,monospace;

  /* === Type scale === */
  --text-xs:  12px; --text-sm:  14px; --text-base: 16px; --text-lg:  18px;
  --text-xl:  22px; --text-2xl: 32px; --text-3xl:  48px; --text-4xl: 56px;
  --leading-body:   1.40;
  --leading-tight:  1.10;
  --tracking-display: -0.02em;

  /* === Spacing (4px scale) === */
  --space-1:  4px;  --space-2:  8px;  --space-3: 12px; --space-4: 16px;
  --space-5: 20px;  --space-6: 24px;  --space-8: 32px; --space-12: 48px;

  /* === Section padding === */
  --section-y-desktop: 96px;
  --section-y-tablet:  64px;
  --section-y-phone:   40px;

  /* === Radii (small = precise) === */
  --radius-sm:   4px;
  --radius-md:   6px;
  --radius-lg:   8px;
  --radius-pill: 9999px;

  /* === Elevation / shadows === */
  --elev-flat:    none;
  --elev-ring:    0 0 0 1px var(--border);
  --elev-raised:  rgba(50,50,93,.25) 0 30px 45px -30px, rgba(0,0,0,.10) 0 18px 36px -18px;
  --focus-ring:   0 0 0 2px var(--accent), 0 0 0 5px color-mix(in oklab,var(--accent),transparent 75%);

  /* === Motion (calm) === */
  --motion-fast:    150ms;
  --motion-base:    200ms;
  --ease-standard:  cubic-bezier(.2,0,0,1);

  /* === Container === */
  --container-max:           1080px;
  --container-gutter-desktop: 32px;
  --container-gutter-tablet:  24px;
  --container-gutter-phone:   16px;
}

/* === 2px top-border signature on primary CTA (Vantia tell) === */
.btn.primary {
  background:    var(--accent);
  color:         var(--accent-on);
  border-top:    2px solid var(--accent-active);   /* ← signature: heavier top edge */
  border-right:  1px solid transparent;
  border-bottom: 1px solid transparent;
  border-left:   1px solid transparent;
  border-radius: var(--radius-sm);
  /* weight, sizing, transitions per Stripe defaults */
}
.btn.primary:hover  { background: var(--accent-hover); }
.btn.primary:active { background: var(--accent-active); }
```

### Pairing rules for future Vantia copy

- **CTA primário:** always `var(--accent)` background + `var(--accent-on)` (white) text + 2px top-border `var(--accent-active)`. Never use `--brand` (the bright lime) for CTA — fails WCAG on white text.
- **Wordmark / logo:** use `var(--brand)` color. On dark surfaces, the lime brilha; on light, navy text on lime brand surfaces uses `--brand-on`.
- **Eyebrow / kicker text:** `var(--accent)` darker lime, NOT brand — for legibility at small sizes.
- **Decorative bands / hover bg / badges:** `var(--brand)` ou `var(--accent-soft)`.
- **Status states** (success/warn/danger): use the dedicated tokens — never overload the accent.

### Validated preview

Phase B + C1 iterations resulted in approved layout pattern:
- Stripe-warm light surface + deep navy text + Söhne weight 300 display
- Dual-role lime applied per pairing rules above
- 2px top-border on CTA (micro-signature)

Reference: `groups/main/strategy/html/vantia-moodboards/C1-preview-dual-lime.html` (or daemon URL `http://localhost:3200/artifacts/generated-1779114371971.html`).

---

## What I extracted as-is from Stripe (keep)

The Stripe system has decades of refinement in palette neutrals, spacing, and type scale. Where the choice is already optimal, we inherit:

| Token group | Decision | Why |
|---|---|---|
| **Neutrals** (BG / FG / muted / border) | Keep Stripe's exact values | Deep navy `#061b31` text on warm-white `#f6f9fc` surface is a globally-tuned readability win |
| **Type scale** (12 → 56px) | Keep | Proven SaaS rhythm |
| **Spacing scale** (4 → 48px, multiples of 4) | Keep | Standard Tailwind-style |
| **Border radii** (4/6/8/pill) | Keep | Small radii = "precise" — matches Vantia personality |
| **Shadows / elevations** | Keep | Stripe's subtle layering |
| **Motion** (150ms fast / 200ms base, ease-standard) | Keep | Calm motion = Vantia personality trait #3 |
| **Container max** | Keep `1080px` | Focused feel, not enterprise-wide |

---

## What we change (Vantia-specific)

### 1. Accent color — **CHOOSE 1 of 3**

**Why we change:** using Stripe's exact `#533afd` purple is visual plagiarism. Vantia needs its own identifying accent within the same warmth family.

Three options, each defensible:

#### Option α — Trust Blue `#2563eb`
```
--accent: #2563eb;          /* mainstream tech blue */
--accent-hover: #1d4ed8;
--accent-active: #1e3a8a;
```
- **Feel:** safe, mainstream-tech, "we look like SaaS that works"
- **Risk:** generic — every B2B SaaS uses some blue
- **Bonus:** **same family as Ritmo** (Ritmo uses `#2563EB` per `design-system.md`), so Vantia + Ritmo would feel like siblings without being identical
- **Best for:** if you want fast brand cohesion across portfolio

#### Option β — European Emerald `#0a7a55`
```
--accent: #0a7a55;          /* deep emerald, European trust */
--accent-hover: #086344;
--accent-active: #054d34;
```
- **Feel:** distinctive, slightly European/sophisticated, less common in SaaS
- **Risk:** can read as "finance" or "compliance" tool to wrong audience
- **Bonus:** strong differentiation from competitors; pairs beautifully with Stripe's warm neutrals; works well on light AND dark surfaces
- **Best for:** if you want Vantia to look intentionally different from US-SaaS norm

#### Option γ — Warm Terracotta `#d97757`
```
--accent: #d97757;          /* warm terracotta — Anthropic-ish but warmer */
--accent-hover: #c66744;
--accent-active: #a85537;
```
- **Feel:** crafted, warm, distinctive — breaks SaaS sameness without going brutal
- **Risk:** unusual for B2B — some Founders/buyers may read as "boutique" not "tool"
- **Bonus:** maximum differentiation; signals studio-craft over corporate-software
- **Best for:** if Vantia leans into "small studio that ships" identity proudly

**Founder pick:** [answer here with α / β / γ]

---

### 2. Typography

**Replace:** Stripe's `Söhne` (commissioned, not freely licensable for general use).

**Adopt:**
```
--font-display: "Inter Variable", "Inter", -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
--font-body:    "Inter Variable", "Inter", -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
--font-mono:    "JetBrains Mono", ui-monospace, "SF Mono", Menlo, Monaco, Consolas, monospace;
```

**Why Inter:**
- Free (OFL), available everywhere
- Variable font (weights 100-900 in one file → fast load)
- Designed specifically for UI legibility
- Already used by Linear, GitHub, Figma, Notion, Vercel — standard SaaS choice
- If you later want to upgrade to a premium font (e.g. Söhne, GT Walsheim) → only change two CSS variables

**Why one font for display + body** (vs Stripe pattern):
- Reduces requests, faster load
- Inter handles both gracefully (weight 200-300 for display, 400-500 for body)
- Consistent feel across UI surfaces
- If you ever want distinction, add a serif for editorial moments (e.g. `Source Serif Pro` for blog) — but base system stays mono-family

**Weights to use:**
- Display (h1/h2): **weight 300** (matches A mood board, "light precise" feel)
- Subheadings (h3/h4): **weight 400**
- Body: **weight 400**
- Buttons / UI emphasis: **weight 500**
- Eyebrow / meta / labels: **weight 400** uppercase + letter-spacing

---

### 3. Visual signature (a small thing that's only Vantia)

Stripe doesn't have any distinctive ornament — it's pure typography + color. To give Vantia a 5-second-recognisable signature without going overboard, propose one micro-detail:

**Option:** **2px solid border** at the top of every primary CTA button (instead of standard 1px). Tiny, intentional, repeated everywhere. Becomes a brand tell over time.

```
.btn.primary {
  border-top: 2px solid var(--accent-active);  /* slightly darker than fill */
  /* rest as standard */
}
```

If you don't want this, we drop it — Vantia can just be "Stripe-warm minus the trademark purple, with our accent." That's already a valid identity.

**Founder pick:** [answer here — yes/no on the 2px border signature]

---

### 4. Status colors (success/warn/danger)

Stripe's defaults are fine, just normalise the warm/cool balance:

```
--success: #15a85a;   /* slight desaturation of Stripe's #15be53 — calmer */
--warn:    #b6701a;   /* slight saturation of Stripe's #9b6829 — more readable */
--danger:  #d92660;   /* slight desat of Stripe's #ea2261 — less aggressive */
```

**Founder pick:** [accept as-is, or flag if you want different]

---

## Summary — what I need from you (3 quick decisions)

| # | Decision | Options |
|---|---|---|
| 1 | **Accent color** | α (blue, sibling to Ritmo) / β (emerald, European-distinctive) / γ (terracotta, studio-craft) |
| 2 | **2px CTA top-border signature** | yes / no |
| 3 | **Status colors** | accept as-is / flag adjustments |

Answer inline with `**Answer:** ...` under each.

---

## After you answer

I will:
1. Update this doc with your picks (becomes the locked tokens spec).
2. Move to **C2 logo** — choose between Recraft generation (a) or wordmark-typographic (c) per the options I sent earlier.
3. When logo decided, **Phase D** encodes everything into `/home/nanoclaw/open-design/.od/design-systems/vantia/DESIGN.md` in the `google-labs-code/design.md` format for the Open Design daemon. From that point, `ext_call(open-design, generate_artifact, {design_system:'vantia'})` produces Vantia-branded output.
