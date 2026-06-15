# Palette: eink-duotone

Near-monochrome **ink-on-paper duotone**, like an e-ink reader or a Monocle spread. One **deep, slightly-colored ink** (not pure black — a dark navy, forest, kraft-brown or dune-warm) sits on one **warm off-white paper**; everything is built from those two tones plus their tints, with at most one tiny accent. Calmer and warmer than `mono-ink`'s pure black-on-white: the ink carries a faint hue and the paper is never clinical white. Pairs natively with the [`eink-magazine`](../visual-styles/eink-magazine.md) visual style.

> This file describes **color behavior**, not HEX values. The specific ink/paper HEX comes from `design_spec.colors` (the eink-magazine style ships five ready duos — see that file). eink-duotone overrides the *usage pattern* of those colors.

> Adapted from the **guizang-ppt-skill** (`op7418/guizang-ppt-skill`) ink+paper color system.

## 1. Special: deviates from deck HEX

eink-duotone reinterprets `design_spec.colors` rather than using each slot literally:

- **Ink** = the deck's darkest color (a *tinted* near-black, e.g. navy `#0A1F3D`, forest `#1A2E1F`, kraft `#2A1E13`) — used for all line work, figures, type, AND as the full-bleed background on hero/divider images.
- **Paper** = the deck's lightest color (a warm off-white, e.g. `#F1EFEA`, `#F0E6D2`) — the dominant background on content images and the text color when on an ink field.
- **Tints** (`*_tint`) — the only permitted mid-tones; used for soft fills, secondary rules, ghosted background numerals. No other greys.
- **Accent** — optional, ≤10% of canvas, a single warm gold or a hue-matched bright tint, on one emphasized element only.

When proposing eink-duotone, the assembled prompt should note: "eink-duotone uses the deck's ink `#XXX` (a tinted near-black) and warm paper `#XXX` as a two-tone system — ink-field images invert (paper-colored marks on the ink background); content images are paper-field. Mid-tones only via tints; accent `#XXX` ≤10% on one element."

## 2. Compatible renderings

| Rendering | Notes |
|---|---|
| ✓✓ editorial | Direct alignment — the magazine-restraint look eink-magazine pairs with |
| ✓✓ ink-notes | Austere hand-lettered version of the same discipline |
| ✓ blueprint | Schematic two-tone works, tint the lines with the ink hue |
| ✓ vector-illustration | Acceptable if kept flat and two-tone (no gradients beyond the faint hero field) |
| ✗ sketch-notes / watercolor / nature / fantasy-animation | Too warm/playful; breaks the e-ink calm |
| ✗ tech-neon / digital-dashboard | Intentionally non-digital, no glow |
| ✗ corporate-photo | Photography can't hold a strict duotone |

---

## 3. Fewshot prompt snippets

**Snippet A — paper-field content diagram (Indigo Porcelain duo)**

> [...rendering paragraph...] Color behavior is eink-duotone: warm off-white paper `#F1F3F5` background (about 80%); all rules, labels, figures and type in deep indigo ink `#0A1F3D` (about 17%); soft fills use the paper-tint `#E4E8EC` only. A single data figure carries a warm gold accent `#C8A24A` (about 3% of canvas). No other greys, no gradients, no shadows — flat e-ink calm. [...container guidance...]

**Snippet B — ink-field hero / chapter divider (Dune duo, inverted)**

> [...rendering paragraph...] Color behavior is eink-duotone inverted for a hero field: full-bleed deep dune ink `#1F1A14` background (about 88%); headline and a giant ghosted serif numeral in warm paper `#F0E6D2`, the numeral at ~6% opacity; a single hairline rule in paper-tint. One small monospace kicker in paper. No photographic texture beyond a whisper-faint radial darkening at the corners. [...container guidance...]
