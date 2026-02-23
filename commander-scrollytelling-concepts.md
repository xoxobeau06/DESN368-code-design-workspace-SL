# Commander x JavaScript Scrollytelling Concepts (Desktop 1440)

## Core Layout Frame (applies to all sections)
- **Canvas:** 12-column grid in 1440 frame, 80px side margins, 24px gutters.
- **Rhythm:** Alternate section heights between dense (`min-height: 110vh`) and spacious (`min-height: 150vh`) blocks.
- **Panel system:** Rounded card-like modules (`16-24px` radius) with layered shadows in light mode and soft border glow in dark mode.
- **Mana accents:** Assign one mana accent per concept and keep it consistent in icon glows, divider lines, and interaction highlights.

---

## 1) Hero Section — 3 Layout Variations

### Variation A — "Command Zone Centerpiece" (single focal card)
**Structure**
- Central oversized "Commander Card" panel (roughly 7 columns wide), vertically centered.
- Left side (2-3 columns): short narrative label stack (theme + subtitle + scroll cue).
- Right side (2-3 columns): compact "deck stats" chips (8 sections, light/dark toggle chip, estimated scroll time).
- Background: low-contrast battlefield texture layer + mana symbols at extreme edges.

**Why it fits your constraints**
- One dominant focal point (center card).
- Strong card metaphor.
- Easy to adapt to light/dark with one theme switch.

### Variation B — "Split Battlefield" (narrative left, visual right)
**Structure**
- Left 5 columns: typography-led story block (title + short pitch + CTA arrow).
- Right 7 columns: stacked card panels in perspective, with top card as current focal point.
- A horizontal "turn timeline" bar runs near the bottom (hero only) hinting at scroll progression.

**Why it fits your constraints**
- Clear focal point on top card while allowing supporting context.
- Feels editorial and readable for desktop.
- Transition-friendly into first content section.

### Variation C — "Deck Fan + Spotlight" (diagonal dynamic)
**Structure**
- Fan of 5-7 card backs diagonally from lower-left to upper-right.
- One selected card pulled forward in spotlight at center-right.
- Small intro copy block anchored top-left.
- Floating mana pips orbit around selected card.

**Why it fits your constraints**
- Dynamic composition without multiple competing focal points.
- Works well with parallax depth layers.
- Instantly communicates "deck/commander" metaphor.

---

## 2) Parallax Concepts (meaningful, not decorative)

### Concept 1 — "Draw Step Depth"
**Narrative meaning:** As you scroll, you are drawing understanding from the deck into active play.

**Layering plan**
- Back layer: card-back stack (slowest movement).
- Mid layer: mana symbol field and battlefield texture.
- Front layer: active lesson card slides upward and scales slightly.

**GSAP feasibility**
- `ScrollTrigger` scrub on `yPercent`, `scale`, and `opacity` by layer.
- Pin hero briefly (`pin: true`) so depth story completes before release.

### Concept 2 — "Priority Stack"
**Narrative meaning:** JavaScript execution stack resolves from top to bottom as you scroll.

**Layering plan**
- Vertical stack of translucent "spell" panels (logs, variables, conditionals, events).
- As scroll advances, top panel resolves (fades/locks in place), next rises to active layer.
- Resolved items move to a side graveyard/archive strip.

**GSAP feasibility**
- Timeline with `scrub` and stepped labels.
- `z-index` swaps + transform transitions.
- Pinned container for deterministic sequencing.

---

## 3) ScrollTrigger Reveal Ideas that Reinforce the Metaphor

- **Summon reveal:** Section title card enters as if cast from hand (slide up + glow burst + settle).
- **Tap/untap cycle:** On enter, key icon rotates 90° to "tapped" state; on leave back, rotates to "untapped".
- **Mana payment reveal:** Cost pips fill one-by-one before content body appears.
- **Stack resolution reveal:** Bullet points reveal in LIFO order (last listed appears first), echoing stack behavior.
- **Card flip reveal:** Dense sections use a front/back flip between metaphor side and JS explanation side.
- **Exile/fade transition:** Previous section cards drift to an exile rail rather than simply disappearing.

---

## 4) Subtle Interactive Ideas (realistic with GSAP)

- **Hover tilt cards:** Small `rotateX/rotateY` with shadow shift and accent edge glow.
- **Mana cursor halo:** Cursor-proximity gradient that changes color by section mana identity.
- **Scroll progress as life counter:** Sticky badge increments/decrements (e.g., 40 to 0 as journey progresses).
- **Micro pulse on key terms:** `console.log`, `let`, `if`, `addEventListener`, `localStorage` gently pulse when entering viewport.
- **Theme shift crossfade:** Smooth token swap between light/dark using CSS vars + GSAP tweened custom properties.
- **"Draw card" click affordance:** Optional click on small deck icon triggers one-card draw animation tied to next section hint.

---

## 5) Visualizing "State Change" in Conditionals

- **Branching battlefield lanes:** One incoming card splits into two lanes (`if`/`else`) with only one lane illuminated based on a toggle state.
- **Rule text mutation:** A card's rules text rewrites in-place when condition flips (`isNight = true`).
- **Token transformation:** Creature token art swaps (e.g., 1/1 to 3/3) to represent changed output state.
- **Threshold meter:** Progress meter crossing a breakpoint triggers animated class/style shift.
- **Stacked snapshots:** Before/after mini-cards slide horizontally, with active state framed in mana glow.

Implementation tip: drive all visuals from a single boolean in demo controls; use GSAP timeline labels (`stateA`, `stateB`) to keep transitions deterministic.

---

## 6) Visualizing "Memory" in localStorage

- **Persistent vault panel:** A locked side panel that stores key-value chips; chips remain visible across sections (sticky component).
- **"Reload proof" animation:** On simulated refresh transition, transient cards disappear but vault chips animate back in unchanged.
- **Save/restore cycle:** "Save" animates values from form card into vault; "Load" animates them back into UI controls.
- **Expiration contrast:** `sessionStorage` chips dissolve on scene change while `localStorage` chips persist.
- **Archive timeline:** Saved entries appear as timestamped runes/cards in a vertical memory log.

Implementation tip: use a tiny demo schema (`theme`, `deckName`, `lastSection`) and animate chip updates whenever values change.

---

## 7) Section-by-Section Density Pattern Suggestion

- **Spacious:** Hero (focus + atmosphere)
- **Dense:** `console.log`
- **Spacious:** variables
- **Dense:** conditionals
- **Spacious:** events
- **Dense:** design tokens
- **Spacious:** localStorage
- **Dense but calm:** closing recap

This alternating rhythm preserves readability and gives each "turn" a distinct pacing feel.

## 8) Mockup Preview

- Open `commander-scrollytelling-mockup.html` in a browser to view a static desktop mockup that demonstrates the hero structure, card panels, light/dark mode toggle, mana accents, and alternating dense/spacious section rhythm.
- If serving locally: run `python3 -m http.server 8000` from repo root and visit `http://localhost:8000/commander-scrollytelling-mockup.html`.
