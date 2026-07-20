# Deck architecture — how `index.html` works

Read this before any code change to the deck.

## Stack

- `index.html` — the entire deck: markup, styles, and one component class. No build step.
- `support.js` — **generated, vendored runtime** (a small React-backed template engine).
  **Never hand-edit it.** Header says: rebuild with `cd dc-runtime && bun run build`.
- At runtime `support.js` pulls **React 18.3.1, ReactDOM 18.3.1 and Babel standalone from
  `unpkg.com`**, and the page pulls fonts from `fonts.googleapis.com`.

> ⚠️ **The deck does not work offline.** Both the runtime and the fonts are CDN-loaded. Test
> on the presentation room's network before Week 13, and keep a fallback (static export or a
> locally vendored copy of React/ReactDOM/Babel).

## Template syntax

Markup lives inside `<x-dc>`. The component class is in the `<script type="text/x-dc">` block.

- `{{ name }}` — interpolates a value returned from `renderVals()`.
- `<sc-if value="{{ flag }}">` — conditional block.
- `<sc-for list="{{ items }}" as="item">` — repeat block.
- `onClick="{{ handler }}"` — binds a function from `renderVals()`.
- `style="{{ someStyle }}"` — the common pattern here: reveal state is delivered as a **style
  string**, not a class.

## State model

```js
this.state = { screen, step, timerOn, timerEnd, now, showCues, stars, scale }
```

- **`screen`** — 0…14, which of the 15 slides is showing. `vals['s' + i] = screen === i`
  drives each slide's `<sc-if>`.
- **`step`** — reveal stage *within* the current slide, reset to 0 on slide change.
- **`scale`** — the stage is a fixed **1920×1080** frame, scaled by
  `min(vw/1920, vh/1080)`. **Design to the 1920×1080 canvas.**

### The step machinery

`stepsFor(screen)` returns how many reveal stages a slide has (default 1):

```js
{ 2:2, 3:2, 4:5, 5:4, 6:4, 7:5, 8:2, 9:4, 10:6, 11:3, 12:3, 13:4 }
```

`nav(+1)` advances `step` until `step + 1 === stepsFor(screen)`, then moves to the next
screen. **If `stepsFor` disagrees with what a slide actually renders, presses get swallowed
(too high) or reveals get skipped (too low).** Update it whenever you add or remove a reveal.

### Reveal helpers

```js
reveal(on, card, delay)                        // opacity + translateY transition
infoReveal(targetScreen, neededStep, delay)    // visible once step >= neededStep
```

`infoReveal` returns *visible* when you're not on the target screen, so off-screen slides
aren't stuck hidden. Bind the result into a slide's `style="{{ token }}"`.

## Slide inventory

| `screen` | Counter | Section label | Speaker | Steps | Content |
| --- | --- | --- | --- | --- | --- |
| 0 | 01/15 | — | Chengxi | 1 | Title, orbit animation, team names |
| 1 | 02/15 | `00 · BRIEFING ROUTE` | Chengxi | 1 | Agenda; 5 clickable route nodes |
| 2 | 03/15 | `01 · WHY LICENSING MATTERS` | Chengxi | 2 | Orbital slot → ITU → IMDA chain |
| 3 | 04/15 | `02 · CURRENT PROCESS` | Chengxi | 2 | Email package; illustrative inbox |
| 4 | 05/15 | `03 · BOTTLENECK` | Chengxi | 5 | 3 issues + objective line |
| 5 | 06/15 | `04 · RECON — SINGAPORE` | Subque | 4 | Singpass/Myinfo, GoBusiness |
| 6 | 07/15 | `05 · RECON — INTERNATIONAL` | Subque | 4 | FCC ICFS, commercial engines |
| 7 | **08/15** | `06 · LITERATURE SYNTHESIS` | Subque | 5 | 3 evidence streams → 3 rules → convergence |
| 8 | 09/15 | `07 · THE PROPOSAL` | Jin Yong | 2 | Before/after flip, four tiers |
| 9 | 10/15 | `08 · WALKTHROUGH` | Jin Yong | 4 | Tier 1–4 tabs |
| 10 | 11/15 | `09 · TELEMETRY` | Pei Qi | 6 | 4 metrics + pilot band |
| 11 | 12/15 | `10 · PAYOFF` | Pei Qi | 3 | IMDA / applicant benefits |
| 12 | 13/15 | `11 · RISK REGISTER` | Rachel | 3 | Engine constraints, cost |
| 13 | 14/15 | `12 · GO / NO-GO` | Rachel | 4 | Features, the ask, closing line |
| 14 | 15/15 | `REFERENCES · IEEE` | Team | 1 | All 20 IEEE references |

**Note the two numbering systems.** The header counter is `screen + 1` of 15. The on-slide
section label is an editorial number that starts at `00` on the agenda slide — so they are
deliberately offset by two from `screen 2` onward. When someone says "slide 8" they usually
mean the **header counter**, i.e. `screen 7`.

## Speaker segments

`segDefs` in `renderVals()` drives the footer buttons; `owners` drives the cue overlay.

| Segment | Speaker | Screens | Reveal beats |
| --- | --- | --- | --- |
| S1 | Chengxi | 0–4 | 11 |
| S2 | Subque | 5–7 | 13 |
| S3 | Jin Yong | 8–9 | 6 |
| S4 | Pei Qi | 10–11 | 9 |
| S5 | Rachel | 12–14 | 8 |

**Total: 47 beats, 46 forward presses for the full deck.**

> ⚠️ **Airtime is a scored rubric criterion.** Beats are a rough proxy for speaking time, and
> they are currently uneven (Subque 13, Jin Yong 6). Jin Yong's two slides are the densest in
> the deck, so the gap is smaller in practice than it looks — but confirm with a timed
> run-through, and rebalance by moving a screen boundary in `segDefs` rather than by padding
> slides.

## Presenter controls

| Key | Action |
| --- | --- |
| `→` / `Space` / `Enter` / `PageDown` | Advance one step or slide |
| `←` / `PageUp` | Back |
| `Home` | Return to title |
| `T` | Toggle countdown timer (`timerMinutes` prop, default **20**) |
| `N` | Toggle delivery-cue overlay (per-slide coaching + segment owner) |
| `R` | Jump straight to the references slide — for Q&A |

Clicking anywhere on the stage that isn't a button or link also advances.

## Slide 7 (counter 08/15) — literature synthesis

Rebuilt to be legible in one pass. Structure:

- **Header** — title plus the framing question (`litQuestion`, visible on arrival).
- **Three `.stream-col` columns**, revealed one per press (`litCol1/2/3`). Each column is a
  distinct *literature*, not a theme: source name → citations → what it demonstrates → the
  design rule it yields (`01`/`02`/`03`) → which platform tier it shapes.
- **`.converge-bar`** (`litConverge`) — the shared finding across all three: every system
  structures routine work and leaves judgement with the regulator → Tier 4.

Design constraints for this slide, learned from the previous version:

- **No charts.** The earlier design used bar graphs whose heights encoded nothing. Anything
  chart-shaped invites "what does that measure?" in Q&A and there was no answer.
- **No ambient motion.** Reveals carry the pacing; the file's own stated motion policy
  reserves animation for a new message, a moving application, or live system status.
- **Evidence → rule → tier must stay traceable.** This slide is where the deck earns the
  "design thinking is illustrated" rubric line: it shows the four tiers were *derived* from
  the literature rather than invented.

Slide-scoped CSS: `.stream-col`, `.stream-head`, `.stream-cite`, `.stream-body`,
`.stream-rule`, `.stream-num`, `.stream-tier`, `.converge-bar`. Delete them if the slide goes.

## Conventions

- Keep slide markup **multi-line and readable**. An earlier revision collapsed this slide into
  single 4,000-character lines and became effectively uneditable.
- Small mono labels defined in CSS classes carry `font-size:...!important` to survive the
  global inline-`style` font-size bumps at the top of the `<style>` block.
- Palette: teal `oklch(0.82 0.13 185)` / `#22e6d9` primary, amber `#ffc857` / `oklch(0.82 0.13
  75)` secondary, red `oklch(0.7 0.15 25)` for problems, green `#61df87`, purple `#ae78f5`.
- Panels: `rgba(17,24,35,0.9)` on `#0a0e14`, borders `#1e2a3a` / `#2a3a50`.
- `prefers-reduced-motion` is already honoured globally — don't bypass it.
