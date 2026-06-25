# GitFut — Design System

> Implemented and live. Source of truth for tokens (also see `app/globals.css`).

## Color strategy

**Committed-to-dark with a reserved-gold prize accent.** The surface is WC26 near-black; GitHub-green is the single action accent (kept well under 10% of surface, Restrained-style for chrome); gold is reserved exclusively for prestige (Gold tier, rating chip). Tier metals (bronze/silver/gold/navy/ivory) live on the card art only.

Neutrals are tinted toward the GitHub-dark blue-hue (not pure black/white).

### Tokens (hex in code; treat as OKLCH-equivalents when refining)
- Canvas `#0d1117` · deep `#010409` · surface `#161b22` / `#21262d` · line `#30363d` · gray `#8b949e`
- Ink `#e6edf3` / dim `#c9d1d9` / soft `#a8b3bd` / faint `#8b949e` / mute `#6e7681`
- Green (action) `#39d353` / hi `#56e06b` / mid `#26a641` / deep `#006d32`
- Gold (prestige, reserved) `#d4af37` / hi `#e9cc74` / deep `#b48811`
- Never pure `#000`/`#fff`; canvas is never `#000000` (disappears on dark feeds).

## Theme

Dark. Scene: a developer at night, dark editor open, glancing at a card that should glow like a rare pack pull on a near-black screen and pop on both dark and light social feeds. The scene forces dark.

## Typography

- Display: **Bebas Neue** — ultra-condensed all-caps, ratings/names/headlines (the WC26 tournament impact).
- UI/body: **Inter** — legible at small sizes.
- Mono: **JetBrains Mono** — the `@handle`, the dev signal.
- Hierarchy via scale + weight; body line length capped.

## Material & elevation

Material hierarchy. Card = only glossy/gradient object (tier art + glow). Panels = matte `#161b22`, hairline `#30363d` borders, no blur. Depth = radial glow + spotlight, not glass. One surgical glass moment max.

## Motion

- Walkout reveal: card rises from dark into a spotlight, tier glow ignites; rare tiers (TOTW/TOTY/Icon) add a confetti burst + key-change; ends on a clean hero freeze (the screenshot frame).
- Ease-out exponential curves; no bounce/elastic; never animate layout props.
- `prefers-reduced-motion` collapses to the freeze frame.
- Ambient: gentle float (mascot/card), pulsing GitHub-contribution-grid motif, gold shimmer for prestige.

## Signature elements

- **Mascot**: real logo PNG (transparent), Octocat-footballer + WC26 ball. Landing hero, loading entertainer, share page. Demoted to a small corner mark on Result.
- **Contribution-grid motif**: faint GitHub-green pulsing grid along the bottom of dark surfaces.
- **Tier glow / spotlight** behind the card.

## Layout

- Landing: type-driven hero (mascot + pill + Bebas headline + giant green `@`-input/CTA) left, card fan right.
- Result: card centered, stat/attribute/playstyle panels flank on desktop, stack below on mobile; card always gets a clean screenshot zone.
- Vary spacing for rhythm; avoid wrapping everything in containers; cards-as-affordance only when truly best.

## Bans (project-specific, on top of global)

Gradient text, side-stripe borders, glassmorphism-as-default, hero-metric template, identical card grids, modal-first, em dashes.
