# SFL Platform Presentation — Project Instructions

Interactive UCS1001 team proposal presentation for a **Satellite Filing & Licensing (SFL)
platform** proposed to IMDA. Single-page app, served from `index.html` via GitHub Pages.

## Read the reference docs before changing anything

The graded source material lives in `docs/`. It is transcribed from assignment files that
were originally in the user's `Downloads` folder — treat `docs/` as the canonical copy and
do not depend on those original paths existing.

| File | What it holds | Read it before |
| --- | --- | --- |
| [docs/report-source.md](docs/report-source.md) | Full Assignment 2 report text and all 20 IEEE references | Touching any slide claim, number, or citation |
| [docs/assignment-brief.md](docs/assignment-brief.md) | CA2a + CA2b task requirements, 20-minute limit, submission rules | Any scope, format, or timing decision |
| [docs/rubrics.md](docs/rubrics.md) | All three rubrics rewritten as actionable checklists | Any content or design decision |
| [docs/deck-architecture.md](docs/deck-architecture.md) | How the deck is wired: slides, steps, reveals, speaker segments | Any code change to `index.html` |

**Minimum before editing slides:** `deck-architecture.md` (so you don't break the step
machinery) and `report-source.md` (so every claim stays traceable).

## Hard rules

1. **Every factual claim on a slide carries a bracketed IEEE citation** (`[5]`, `[9], [10]`)
   that resolves to the reference list on the final slide (`s14`). The presentation rubric
   scores citation adherence directly. Never introduce a claim that isn't in
   `docs/report-source.md`.
2. **Never invent data.** No chart, bar, percentage, or figure unless it appears in the
   report with a source. Decorative shapes that look like data are worse than no chart —
   a grader can ask what they measure.
3. **Motion is reserved** for a new message, a moving application, or live system status
   (this rule is already written at the top of the `<style>` block in `index.html`).
   Reveal transitions carry pacing; ambient loops are not decoration budget.
4. **Preserve the five speaker segments.** Airtime balance across the five team members is
   an explicit rubric criterion. Changing slide counts shifts airtime — check
   `deck-architecture.md` before adding or removing a screen.
5. **The whole deck must fit 20 minutes**, strictly enforced by the tutor. Each added
   reveal step is another press and another beat of speaking time.

## Working conventions

- Slide markup is inline-styled HTML inside `<sc-if>` blocks. **Keep it multi-line and
  readable** — do not collapse a slide into one long line.
- `stepsFor(screen)` in the component class must match the number of reveal stages a slide
  actually uses, or the deck will swallow or skip presses.
- Reveal styles are produced by `infoReveal(screen, neededStep, delay)` in `renderVals()`.
- The stage is a fixed 1920×1080 frame scaled to fit the viewport; design to that canvas.
- Remove CSS for elements you delete. Several classes exist solely for one slide.

## Do not

- Do not commit or push unless explicitly asked.
- Do not add external runtime dependencies. `support.js` is a generated, vendored runtime —
  never hand-edit it.
