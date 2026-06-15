# Visual style: eink-magazine

"电子墨水 × Monocle 杂志" — a restrained, editorial e-ink aesthetic: a deep **ink** field and a warm **paper** field, big serif-display headlines, monospace metadata chrome top & bottom, and a deliberate **dark ↔ light page rhythm**. Structure comes entirely from **type scale, hairline rules and whitespace — never cards or shadows**. For keynotes, founder talks, launch decks, and any "分享会 / 发布会" that should feel like a printed magazine rather than a slide template.

> Design language adapted from the **guizang-ppt-skill** (`op7418/guizang-ppt-skill`, the "电子杂志 × 电子墨水" web-deck generator). Its signature WebGL fluid background and horizontal-swipe interactivity are web-only and **cannot** survive in PPTX; this style ports the static half — palette, typography, chrome, layout rhythm — and substitutes a subtle SVG gradient/grain on ink-field hero pages for the live shader.

---

## 1. Shape & decoration

- Shape language: strictly rectilinear. **No cards, no rounded panels, no shadows.** Separation is done with **hairline rules** (`<line>` / 1px `<rect>`, opacity 0.2–0.35) and whitespace.
- Decoration: a short **kicker / eyebrow** in monospace above headlines; thin rules; an oversized faint "ghost" numeral/letter behind hero content (serif, opacity ~0.05); optional accent tick-mark. Typographic, not graphic.
- **Magazine chrome (signature):** every non-cover page carries a top **meta row** (`栏目 · 日期` left, `ACT · 页/总` right) and a bottom **footer** (page descriptor left, `— · —` right) — both in small uppercase monospace, opacity ~0.6. This frame is what makes it read as a magazine.
- Whitespace: generous and intentional. A `breathing` page is mostly empty with one idea; `dense` pages use columns/grids but still no cards.

## 2. Typography character

The defining move is a **three-font triad** with hard role contrast:

- **Display serif** for headlines, big numbers, pull-quotes — large, tight leading, the visual anchor.
- **Monospace** for kickers, the chrome meta/footer, labels, page numbers — small, uppercase, wide letter-spacing.
- **Clean sans** for body and captions.

Type scale is aggressive: hero/cover headline ~3–5× body; chapter-divider numeral huge; data figures huge. Hierarchy is carried by *size + family*, not weight alone.

> Families are locked at confirmation `g`. This style asks for the **serif-display + monospace + sans** triad. PPT-safe realization (PPTX has no web-font fallback): display `Georgia, "Songti SC", SimSun, serif`; mono `Consolas, "Courier New", monospace`; body `"Microsoft YaHei", "PingFang SC", Arial, sans-serif`. (The source skill uses Playfair Display / Noto Serif SC / IBM Plex Mono / Noto Sans SC — only viable if the deck notes "requires font install or PPTX embed".)

## 3. Using the deck's colors

- **Two-tone, near-monochrome.** One deep **ink** hue + one warm **paper** hue carry ~95% of every page; at most one restrained accent for a single emphasized figure or rule.
- **Dark ↔ light rhythm is the soul of this style.** Cover, chapter dividers, big-quotes and section transitions are **ink-field** (paper-colored text on the ink background); content pages are **paper-field** (ink text on paper). Alternate so no 3 consecutive pages share a field; place an ink-field hero roughly every 3–4 pages.
- Color marks structure and emphasis only — no decorative fills. Pairs naturally with the [`eink-duotone`](../image-palettes/eink-duotone.md) palette.

## 4. Texture / elevation

- **Flat. Zero elevation.** No drop shadows, no floating cards — that is the whole point.
- The only "texture" is on ink-field hero pages: a very subtle SVG `radialGradient` / `linearGradient` (and optional faint grain) standing in for the source skill's WebGL fluid background. Keep it whisper-quiet; content stays crisp and flat.

## 5. Paired image-rendering

`editorial` — magazine-style, restrained, monochrome-leaning infographic look for AI images (or `ink-notes` for the most austere decks).

## 6. Recommended color schemes (suggest at confirmation `e`)

Per catalog rule a style locks no palette; these are the source skill's five ink+paper duos, offered as ready `design_spec.colors` choices. Set `bg`/light surfaces from **paper**, body text + ink-field backgrounds from **ink**, with a `*_tint` for soft fills.

| Scheme | ink | paper | paper-tint | ink-tint | Best for |
|---|---|---|---|---|---|
| 墨水经典 Ink Classic | `#0A0A0B` | `#F1EFEA` | `#E8E5DE` | `#18181A` | Universal / business / safe default (Monocle) |
| 靛蓝瓷 Indigo Porcelain | `#0A1F3D` | `#F1F3F5` | `#E4E8EC` | `#152A4A` | Tech / research / data / launches |
| 森林墨 Forest Ink | `#1A2E1F` | `#F5F1E8` | `#ECE7DA` | `#253D2C` | Nature / sustainability / culture |
| 牛皮纸 Kraft Paper | `#2A1E13` | `#EEDFC7` | `#E0D0B6` | `#3A2A1D` | Humanities / reading / heritage / indie |
| 沙丘 Dune | `#1F1A14` | `#F0E6D2` | `#E3D7BF` | `#2D2620` | Art / design / fashion / aesthetic-first |

A single accent (e.g. a warm gold `#C8A24A`, or a hue-matched bright tint) may be added for one emphasized figure per page — keep it under ~10% of canvas.

## 7. Pairs well with

Any mode, but especially `narrative` and `showcase` (the dark/light hero rhythm suits a told story). For a data-heavy briefing, keep the chrome and serif figures but lean on paper-field pages.
