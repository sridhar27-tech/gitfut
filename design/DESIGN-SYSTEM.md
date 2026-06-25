# GitFut — Design System

> Status: **Locked** (design direction). Stat content & tier-gating numbers pending the stats algorithm.
> Source of truth for the visual + UX direction. Card itself is out of scope — it arrives as a finished image.

---

## 1. Product

GitFut: enter your **GitHub username** → get a **FIFA-Ultimate-Team-style collectible card** built from your GitHub stats → **share it**.

- **Primary goal:** shareability / virality. People must *want* to screenshot their card and post it to start a trend.
- **Cultural anchor:** FIFA **World Cup 26** (USA/Canada/Mexico). We borrow WC26's **color palette only** (black/white/gray/gold) — not its typeface or IP.
- **Tone:** premium FUT prestige **+** playful dev humor (set by the mascot). Not stiff-corporate.

### The card (out of scope)
The card is a **finished rendered image (PNG/SVG) returned by a service** — a black box. We design the **stage around it**: place it, frame it, glow it, animate its reveal, put it on the share page. We never touch its internals.

---

## 2. Scope — Screens

1. **Landing** — sell the vibe, drive the one action (enter username).
2. **Loading** — indeterminate wait while the card image generates.
3. **Reveal** — the dramatic "here's your card" moment.
4. **Result** — the payoff + share surfaces.
5. **Public share page** (`gitfut.com/@user`) — what a *visitor* sees from a shared link; re-pitches "make your own."

No leaderboards / profiles / compare for v1.

---

## 3. Color System

Three groups, kept separate so they never fight:

### Signature — GitHub green = "the action"
Used on: logo, username input + focus glow, Generate CTA, links, success states, contribution-graph motif.
| Token | Hex |
|---|---|
| `--green` | `#39D353` |
| `--green-mid` | `#26A641` |
| `--green-deep` | `#006D32` |

### WC26 spine = "the luxury frame"
| Token | Hex | Use |
|---|---|---|
| `--black` | `#0D1117` | canvas (GitHub-dark == WC26 black) |
| `--black-deep` | `#010409` | deepest fields |
| `--surface-1` | `#161B22` | panels |
| `--surface-2` | `#21262D` | elevated panels |
| `--border` | `#30363D` | hairline borders |
| `--gray` | `#8B949E` | muted text |
| `--offwhite` | `#E6EDF3` | body text |
| `--gold` | `#D4AF37` | prestige metal (reserved) |
| `--gold-bright` | `#E9CC74` | gold highlight |

> **Never pure `#000000`** as canvas — disappears on dark social feeds and causes halation. Use `#0D1117`.

### Card tier metals (reference only — card is an image)
Bronze `#CD7F32` · Silver `#C0C0C0` · Gold `#E9CC74→#B48811` · TOTY navy `#0A1428`+gold · Legend ivory `#F5F0E1`+gold.

---

## 4. Typography

| Role | Typeface | Use |
|---|---|---|
| Display | **Bebas Neue** | ratings, names, headlines, scoreboard numbers (ultra-condensed all-caps, the WC26-impact feel) |
| UI / Body | **Inter** | buttons, labels, paragraphs, stat labels |
| Mono | **JetBrains Mono** | the `@handle`, `gitfut.com` — the "we speak GitHub" cue |

(We do **not** use the official FWC26 typeface — IP-restricted. Bebas Neue evokes the character legally.)

---

## 5. Material & Surface Language

**Principle: material hierarchy — the card is the only glossy, high-material object; everything else is matte and recedes.** (Gallery rule: rich painting, flat matte wall.)

- **Panels:** matte near-flat dark (`--surface-1`), hairline `--border`, **no blur**. Calm, GitHub-native, screenshots clean.
- **Sporty/premium energy** comes from **stat typography** (Bebas condensed numbers, label-above-value, thin green/gold rules — scoreboard feel), not from panel texture.
- **Depth = light, not glass:** soft radial glows (green ambient on landing; tier-color glow behind the card on reveal/result). Glow survives screenshots; glass turns to grey soup.
- **Glass used once, surgically** — the floating share bar overlaying the card on Result. One accent, not a system.
- **Buttons:** solid green CTA (pops against matte dark).

Rationale: serves shareability (matte = clean screenshots, card always wins), premium-FUT (light/glow + condensed type = the WC26 broadcast way), and dodges the overused glassmorphism "generic AI" look.

---

## 6. Mascot

**Octocat-as-footballer** — black octopus mascot kicking the official WC26 **Trionda** ball (red/green/blue host-nation colors + gold "26" trophy emblem). One image = the whole concept (GitHub × WC26). Playful, meme-able.

Placement:
- **Landing** — hero character (explains the concept with zero copy).
- **Loading** — kicking the ball + rotating football-git pun lines.
- **Public share page** — present (brand + conversion).
- **Result** — demoted to small / footer (card is king).

Loading pun bank (seed): "Calculating your xG (eXpected Greatness)…", "Checking VAR (Version & Review)…", "Counting clean sheets (zero-bug commits)…", "Measuring your PRs (Penalty Resistance)…".

---

## 7. Rarity Tiers

Bronze → Silver → Gold → **TOTY** → **Legend**. Gated by overall rating (trigger numbers TBD with algorithm).

Finish escalates: matte → sheen → metallic → navy-crystal+gold → ivory-holographic. The tier ladder is the **viral mechanic** — rare frames are what people screenshot.

(Tier visuals live on the card image; listed here for system coherence.)

---

## 8. Screen Specs

### Landing
- Type-driven **WC26 hero** (big Bebas condensed headline + one green value-prop line).
- **Mascot** as hero character.
- **Giant glowing green username input** = the unmistakable focal action, with single Generate CTA.
- Optional: faint atmospheric "mystery card" behind, low opacity.

### Loading
- Mascot kicking the ball.
- Rotating catchy **football-git pun** lines.
- Indeterminate (card generating server-side).

### Reveal — walkout/rise
- Card **rises from darkness into a spotlight**, tier glow igniting, scaling to hero position, locking with a clean freeze.
- **Tier-scaled spectacle:** Bronze/Silver = restrained rise; **TOTY/Legend = full burst** (light explosion + confetti + audio key-change).
- **Ends on a clean, perfectly-framed hero shot** = the screenshot frame.
- **Mandatory `prefers-reduced-motion` path:** cross-fade to the same hero freeze, no shake/particles.

### Result
- **Card centered**; **stat panels + explanations flank left/right (desktop)**.
- **Mobile:** card alone on top in a clean screenshot zone; stat panels **stacked below**. Same content, responsive rearrange — card always gets a clean hero moment.
- Stat content & explanations TBD with the algorithm (design the slots now, fill later).
- Mascot small/footer.
- Share surfaces (see §9).

### Public share page (`gitfut.com/@user`)
- Card hero + stats + mascot + **"make your own" CTA** (closes the viral loop).
- **Dynamic OG image** (1200×630, 1.91:1): portrait card centered on the canvas with branded gutters + watermark (`gitfut.com/@user`). Server-rendered (`@vercel/og`/Satori) so links render rich previews on X/LinkedIn/Discord/iMessage.
- Set `twitter:card=summary_large_image` explicitly; absolute `metadataBase`; cache-bust OG via stats-hash query.

---

## 9. Share UX

- **Primary:** native **Web Share API** sheet (mobile) — the only smooth path to Instagram Stories; feature-detect `navigator.canShare({files})`.
- **Platform row:** X (`/intent/tweet`), LinkedIn (`share-offsite`), WhatsApp, Instagram (image-file path).
- **Fallbacks:** `Download card` (server-rendered image, single source of truth) + `Copy link`.
- **Card is self-contained** (tier glow + soft drop shadow + light hairline) so it pops on **both** dark (X/IG) and light (LinkedIn) feeds.
- Pre-filled share text leads with the brag; seed **#GitFut**; tag shares `?ref={username}` to close the loop.

---

## 10. Open Decisions (pending algorithm)

- The six stat concepts + abbreviations, the position/archetype, and the overall-rating formula.
- Tier-gating numbers (what rating = which tier).
- Whether the Result/share screens surface a **percentile + archetype** line (research: single biggest share driver — recommend yes, design the slot).
