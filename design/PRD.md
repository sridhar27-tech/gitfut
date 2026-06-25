# GitFut — PRD: Design-Layer Rebuild

> **Status:** Ready for build · **Branch:** `design` · **Scope:** UI/design layer rebuild on top of the existing scoring engine.
> **Local PRD** (not published to GitHub, per request). Companion to [`DESIGN-SYSTEM.md`](./DESIGN-SYSTEM.md).

---

## Problem Statement

I have a working GitFut MVP: enter a GitHub username, get a FIFA-Ultimate-Team-style player card rated out of 99, built from real GitHub stats. The **engine is excellent** — a deterministic scoring algorithm that derives six stats, an overall rating, a card tier (bronze → icon), a position, an archetype, and playstyles from real GitHub data.

But the **design is wrong for what this product needs to be**. The MVP looks like a generic coral/purple dark-mode SaaS tool. It has:

- the wrong brand color (coral `#ff4d5e` instead of GitHub green),
- no cultural anchor (the product is a 2026 World Cup × GitHub mashup, but nothing says "World Cup"),
- no mascot / no personality,
- no reveal moment (the card just slides in — no dopamine),
- weak sharing (X-only, no rich link previews, no native share sheet).

The product's **entire reason to exist is shareability** — people screenshotting their card and posting it to start a trend. The current design does not earn the share. A card nobody wants to post is a dead product.

## Solution

Rebuild the **design layer** — every screen, component, and visual token — on top of the untouched scoring engine, implementing the locked GitFut design system:

- **GitHub green** as the signature ("the action") + **World Cup 26 palette** (black / white / gray / gold) as the luxury spine.
- An **Octocat-footballer mascot** kicking the WC26 ball — the brand face on landing, loading, and the public share page.
- A **walkout/rise reveal** with tier-scaled spectacle (bronze = restrained, TOTY/Legend = full burst + confetti).
- **Material hierarchy**: the card is the only glossy hero; everything else is matte and recedes; depth comes from light/glow, not glassmorphism.
- **Bulletproof sharing**: native Web Share API + multi-platform intents + a dynamically-generated Open Graph image so shared links render rich previews everywhere.

The engine stays. The skin, the soul, and the share loop get rebuilt to be unmistakably **GitFut**.

## User Stories

### Discovery & Landing
1. As a visitor, I want to immediately understand "this turns my GitHub into a World Cup card," so that I get the concept in under three seconds without reading.
2. As a visitor, I want to see the mascot (Octocat kicking the WC26 ball) on the landing screen, so that the GitHub × World Cup mashup is obvious and charming.
3. As a visitor, I want one giant, glowing green username input as the unmistakable focal action, so that I know exactly what to do.
4. As a visitor, I want to see example cards or famous-dev shortcuts, so that I can try it without my own profile.
5. As a visitor on mobile, I want the landing to stack cleanly and the input to be reachable, so that the phone experience is first-class (most shares are opened on phones).
6. As a visitor, I want a tasteful "how it works" affordance, so that I can understand the scoring without it cluttering the hero.

### Generating / Loading
7. As a user who just submitted my username, I want the mascot kicking the ball plus a rotating football-git pun ("Measuring your PRs — Penalty Resistance…"), so that the wait is entertaining, not anxious.
8. As a user, I want the loading state to feel intentional and branded, so that even the delay reinforces the product personality.
9. As a user, I want clear, friendly error states (user not found, rate-limited, GitHub down), so that failure never feels broken or hostile.

### The Reveal
10. As a user, I want my card to rise out of darkness into a spotlight with its tier glow igniting, so that getting my card feels like a "drop," not a page load.
11. As a user with a rare card (TOTY/Legend), I want extra spectacle — a light burst, confetti, an audio/visual key-change — so that rarity is visibly earned and worth screenshotting.
12. As a user with a common card (bronze/silver), I want a tasteful, restrained reveal, so that it still feels good without faking rarity.
13. As a user, I want the reveal to end on a clean, perfectly-framed hero shot of my card, so that the final frame is the screenshot I want to post.
14. As a user who prefers reduced motion, I want a calm cross-fade to the same hero frame, so that the experience is accessible and never nauseating.

### The Result
15. As a user, I want my card centered with my stats and their explanations flanking it (desktop) or stacked below it (mobile), so that I understand what each number means.
16. As a user, I want to see my overall rating, position, archetype, and tier prominently, so that I know my "identity" at a glance.
17. As a user, I want my percentile/standing surfaced ("hall-of-fame maintainer," "top-tier"), so that I have a brag worth sharing.
18. As a user, I want to see my playstyles and derived attributes (skill moves, weak foot, work rate), so that the card feels deep and personal.
19. As a user on mobile, I want my card alone in a clean screenshot zone at the top, so that I can screenshot it without UI chrome bleeding in.
20. As a user, I want the mascot to step aside on the result screen, so that my card is the unambiguous hero.

### Sharing (the viral loop)
21. As a user, I want a single prominent "Share" button that opens my phone's native share sheet, so that posting takes one tap.
22. As a user, I want direct share buttons for X, LinkedIn, WhatsApp, and Instagram, so that I can post to my platform of choice.
23. As a user, I want to download my card as a high-resolution image, so that I can post it anywhere or save it.
24. As a user, I want to copy a link to my card, so that I can paste it into any chat.
25. As a user, I want pre-filled share text that leads with my brag and includes the GitFut hashtag, so that posting is effortless and on-brand.
26. As a person who clicks a shared GitFut link on X/LinkedIn/Discord/iMessage, I want a rich preview showing the card, the username, and GitFut branding, so that the link is enticing before I even click.
27. As a person who lands on someone's public card page, I want to see their card plus an obvious "make your own" call-to-action, so that the loop pulls me in.
28. As a user, I want my card to pop whether it's on a dark feed (X/IG) or a light feed (LinkedIn), so that it never disappears into the background.

### Brand & System
29. As the product owner, I want every screen driven by a single set of design tokens, so that the brand is consistent and future changes are one-file edits.
30. As the product owner, I want GitHub green reserved for "the action" and gold reserved for prestige, so that the two never clash and gold stays meaningful.
31. As the product owner, I want the mascot rendered as a reusable asset/component, so that it can appear across screens consistently.
32. As a user on any device, I want the type system (condensed display, clean UI, mono handle) to read clearly at every size, so that the product feels crafted.

### Accessibility & Quality
33. As a user relying on a screen reader, I want the card's stats and rating exposed as text, so that the experience isn't image-only.
34. As a colorblind user, I want tier identity conveyed by label + icon + luminance, not color alone, so that I can tell tiers apart.
35. As a keyboard user, I want the input, CTA, and share actions fully operable without a mouse, so that the app is usable for everyone.

## Implementation Decisions

### Foundational decision: the engine is untouchable
The scoring engine (`lib/scoring/*`) and GitHub data layer (`lib/github/*`) are **kept as-is** and treated as a stable, deep dependency. The rebuild touches only the **UI/design layer**: design tokens, fonts, screens, components, the reveal, the share infrastructure, and the OG image. The engine already produces everything the UI needs: six stats, overall, position, finish/tier, archetype, playstyles, derived attributes.

> **Correction captured during exploration:** the card is rendered as an **HTML/CSS overlay on a per-tier PNG**, *not* a flat returned image. This is a benefit — the reveal animation and tier glow can be done in-DOM, and the card remains restyleable.

### Module: Design Tokens (deep module — the keystone)
A single source of truth for color, type, spacing, glow, and motion tokens, consumed by every screen via Tailwind v4 `@theme`. This is the deepest, highest-leverage module: a simple interface (CSS custom properties) encapsulating the entire visual identity. Changing the brand = changing this one module.

- **Color contract:** green (`#39D353` / `#26A641` / `#006D32`) = action; WC26 spine (`#0D1117` canvas, `#161B22`/`#21262D` surfaces, `#8B949E` gray, `#E6EDF3` ink, gold `#D4AF37`/`#E9CC74` prestige); tier metals reference-only.
- **Type contract:** display (Bebas Neue), UI (Inter), mono (JetBrains Mono).
- **Never** pure `#000000` as canvas.

### Module: Mascot
A reusable mascot asset + thin presentational component with size/pose variants. Appears on landing (hero), loading (animated kick), and public share page. Absent/minimized on the result screen.

### Module: Reveal Sequencer (deep module — testable in isolation)
Encapsulates the reveal as a **tier-driven state machine**: takes a tier, returns a timed sequence of phases. The animation rendering subscribes to phase changes; the sequencing logic is pure and unit-testable without a DOM. Honors `prefers-reduced-motion` by collapsing to a single `freeze` phase.

> Encodes a decision more precisely than prose — phase shape (illustrative, from the design exploration):
> ```ts
> type RevealPhase = "idle" | "rise" | "ignite" | "burst" | "freeze";
> // Tier scales spectacle: commons skip "burst".
> const sequenceFor = (tier: Tier, reducedMotion: boolean): RevealStep[] => {
>   if (reducedMotion) return [{ phase: "freeze", at: 0 }];
>   const base: RevealStep[] = [
>     { phase: "rise",   at: 0 },
>     { phase: "ignite", at: 600 },   // tier glow blooms
>     { phase: "freeze", at: 1400 },  // clean hero shot = the screenshot frame
>   ];
>   if (tier === "toty" || tier === "icon") {
>     base.splice(2, 0, { phase: "burst", at: 1100 }); // light explosion + confetti + key-change
>   }
>   return base;
> };
> ```
> Only `sequenceFor` is tested; the visual layer is not.

### Module: Share Service (deep module — testable in isolation)
Encapsulates all share-target logic behind a simple interface. Pure functions that, given a card + username, produce: native-share payload, per-platform intent URLs (X `/intent/tweet`, LinkedIn `share-offsite`, WhatsApp, Instagram-via-file), pre-filled share text (brag-led, hashtagged), and the canonical card-page URL. No DOM, no side effects in the core — the React layer wires the gestures.

- **Decision:** native Web Share API is the primary path (`navigator.canShare({ files })` feature-detected separately); platform intents are fallbacks; `AbortError` is treated as benign (no error toast).
- **Decision:** X intent uses `/intent/tweet` (not `/intent/post` — avoids the mobile redirect loop).
- **Decision:** card image is self-contained (tier glow + soft drop shadow + hairline) so it survives both dark and light feeds.

### Module: OG Image Generator (deep module)
A dynamically-rendered Open Graph image for the public card page. Composes the portrait card centered on a 1200×630 (1.91:1) canvas with branded gutters + a `gitfut.com/@user` watermark. Server-rendered (Satori / `@vercel/og`) so it works without client JS (iMessage requirement).

- **Decision:** set `twitter:card=summary_large_image` explicitly; absolute `metadataBase`; cache-bust the OG via a stats-hash query so a stale scraper cache refreshes when stats change.
- **Constraint captured:** Satori is flexbox-only and needs a bundled font + a Noto fallback (non-Latin usernames must not render as tofu).

### Module: Screens (presentational composition)
Four screens + the public card page, each composing the modules above:
- **Landing** — type-driven WC26 hero + mascot + giant green input + sample shortcuts.
- **Loading** — mascot kick + rotating pun bank.
- **Reveal** — driven by the Reveal Sequencer.
- **Result** — card centered, stat/attribute/playstyle panels flanking (desktop) / stacked (mobile); mascot minimized.
- **Public card page** (`/u/[username]` equivalent) — card hero + stats + mascot + "make your own" CTA + OG metadata.

### Module: Loading Pun Bank
A small, pure data module: a list of football-git puns, deterministically selected (e.g. hashed by username so the same user sees a stable line, or rotated). Trivial to extend, isolated from the loading view.

### Architectural decisions
- Single token layer drives all screens (one-file rebrand capability).
- Reveal + Share + OG + Pun-bank are **pure/deep modules** with thin React wrappers, so the logic is testable without rendering.
- Material hierarchy enforced by convention: only the card uses glossy/gradient material; panels are matte; depth via light/glow.
- Reduced-motion is a first-class path, not an afterthought.

## Testing Decisions

**What makes a good test here:** test *external behavior and decisions*, not rendering or implementation details. We do not snapshot-test pixels or assert on class names. We test the pure logic that encodes product decisions — the modules with simple inputs and deterministic outputs.

**Modules to test (recommended):**
1. **Reveal Sequencer** — given each tier + reduced-motion flag, assert the produced phase sequence (commons omit `burst`; TOTY/Legend include it; reduced-motion collapses to a single `freeze`). Pure function, no DOM.
2. **Share Service** — given a card + username, assert the generated intent URLs are well-formed and platform-correct, the share text leads with the brag and includes the hashtag, and the canonical URL is right. Assert `/intent/tweet` (not `/intent/post`).
3. **OG metadata/URL builder** — assert the OG image URL, dimensions metadata, `twitter:card` value, and stats-hash cache-bust are produced correctly.
4. **Loading Pun Bank selector** — assert deterministic, stable selection for a given username and that all entries are reachable.

**Out of test scope:** the animation rendering itself, the visual appearance of the card, Tailwind token values (config, not behavior), and the engine (already exists, separately owned).

**Prior art:** the existing `lib/scoring` engine is already a pure, deterministic module — the same testing posture (pure input → asserted output, no rendering) applies to the new Reveal/Share/OG/Pun modules. Mirror that style.

> **Confirm with developer:** which of the four modules above to write tests for now vs. defer. Default recommendation: test Reveal Sequencer + Share Service first (they encode the most product-critical, regression-prone decisions).

## Out of Scope

- **The scoring algorithm and GitHub data layer** — kept as-is, not modified.
- **Leaderboards, profiles, head-to-head card comparison** — not in v1.
- **Auth / accounts / saved cards** — the product stays stateless (username in, card out).
- **Redesigning the card's internal layout** — the existing card composition is retained; only its framing, glow, reveal, and surrounding chrome change. (A future PRD may restyle the card itself.)
- **The stats algorithm content decisions** (which six stats, the formula) — already decided and built.
- **Backend/infra changes** beyond what the OG image generation requires.
- **Monetization.**

## Further Notes

- **Highest-ROI first step:** the entire app is Tailwind v4 `@theme`-token-driven, so a token + font swap re-skins everything from essentially one file. Even within a "full rebuild," landing the token layer first gives an immediate, dramatic on-brand transformation to iterate against.
- **The mascot is the differentiator.** The engine is strong but invisible; the mascot is the face that makes the product *charming* and screenshot-worthy. Treat it as a first-class brand asset, not decoration.
- **The reveal and the OG image are the two virality multipliers.** The reveal earns the screenshot; the OG image earns the click on the shared link. Neither exists today. They are where "good product" becomes "trend."
- **Tone:** premium FUT prestige + playful dev humor (set by the mascot). Avoid stiff-corporate; avoid the overused glassmorphism "generic AI" look.
- **Pun bank seeds:** "Calculating your xG (eXpected Greatness)…", "Checking VAR (Version & Review)…", "Counting clean sheets (zero-bug commits)…", "Measuring your PRs (Penalty Resistance)…".
- **Open question (low priority):** reconcile the existing "scout/scout report" copy theme with the World Cup / mascot tone — decide whether "scouting" stays the metaphor or yields to a more World-Cup-native framing.
