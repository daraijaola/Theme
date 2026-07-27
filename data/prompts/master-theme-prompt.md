# Master Theme Prompt
> The reusable prompt for any theme. This is, in human form, roughly
> what our agent will eventually do automatically. Replace `[THEME]`.

---

Build a single self-contained landing page (one HTML file, no libraries,
no external images, works offline) themed **[THEME]**.

## PHASE 1 — RESEARCH. Do not write a line of code yet.

Research **[THEME]** rigorously, including how it actually *looks*, not
just how it's described:

- **Cultural root** — where it came from, who made it, what it meant.
- **Visual DNA from real references** — study actual photographs, real
  artifacts, real implementations, at least 5–8 distinct samples so you
  see the *range*, not one cliché. Note what recurs and what varies.
- **Two separate colour systems** — the theme's *graphics* palette
  (print, type, artwork) and its *lighting/environment* palette. These
  are usually different. Derive hex values from real sources.
- **Typography DNA** — real letterforms, weight, tracking, case,
  hierarchy logic.
- **Material & texture DNA** — what surfaces exist in this world, and how
  each translates into CSS.
- **Motion DNA** — the rhythm, speed, and weight of movement.
- **Anti-slop guardrails** — an explicit list of the clichés a lazy
  attempt would reach for. Name what the theme is NOT.

Output this research as a short spec before building. Surprising details
are what separate real from generic — keep them.

## PHASE 2 — DESIGN PRINCIPLE

**Do not illustrate the theme. Embed it.** The page should not be a
picture of [THEME]; it should be a normal, useful page that *feels* like
[THEME] through typography, colour, light, texture, motion, copy voice,
and layout rhythm. Pick a neutral subject that suits the mood. A literal
artifact is allowed only if it earns its place as a design element.

## PHASE 3 — CRAFT STANDARD

Apply, where the theme calls for them:

- **Light behaviour** — a defined source and direction; additive light
  (`plus-lighter` inside `isolation: isolate`); bloom spilling from
  bright points; halation on hot highlights.
- **Realism through relationships** — grounding/contact shadows, bounce
  light and colour bleed, occlusion in crevices, falloff with distance,
  rim light at grazing angles.
- **Imperfection** — nothing uniform. Jitter, variation, deliberate
  flaws. Uniformity is the smell of fake.
- **A lens** — grain, colour grade, vignette, selective depth of field.
  Photographed, not drawn.
- **Motion grammar** — easing, arcs not straight lines, follow-through
  and phase-offset lag, secondary action, attack-fast/decay-slow for
  light, and **no two layers sharing a clock**. Prefer noise- and
  spring-driven JS over looping keyframes.
- **Performance** — heavy particles on one canvas, `transform`/`opacity`
  only, disciplined `will-change`.
- **Accessibility** — real contrast, `prefers-reduced-motion` and
  `prefers-reduced-transparency` fallbacks, focus states, semantic HTML.

## PHASE 4 — LAYOUT QUALITY

Hierarchy over evenness. Dramatic type-scale contrast, generous
asymmetric whitespace, one clear focal element, restrained shadow use,
elevation through surface change rather than borders everywhere. Evenly
spaced equal-weight blocks read as a template — avoid that.

## PHASE 5 — SELF-CRITIQUE BEFORE DELIVERING

Name faults precisely: *"No follow-through — the X is rigid while Y
moves; fix by offsetting its phase."* Never "make it better." Check:

- Did I reach for any cliché on my own anti-slop list?
- Is the theme carried by design language, or did I illustrate it?
- Does every element relate to the others through light?
- Does anything loop visibly?
- Would this pass as made by a specialist studio in this style, or does
  it look like a template with a colour swap?

Fix what you find, then deliver.

---

## Addendum — hard-won engine rules

From `data/protocol/director-protocol.md`. Apply before choosing an
architecture:

- Detect the render engine first. `backdrop-filter: url(#svgFilter)` is
  Chromium-only and is dropped **silently** elsewhere.
- Write falsifiable kill-tests per feature before building.
- Specify the background from the effect's requirements first — an
  effect that transforms a backdrop is only visible where the backdrop
  has detail at the effect's spatial scale.
- Build geometry first, then stack the material back-to-front,
  screenshotting after every layer.
- Verify magnitudes by looking. Opacities that look sane in code are
  routinely below perceptual threshold.
