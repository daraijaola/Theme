# Director Protocol
> Extracted from a post-mortem written by a coding model after being
> guided step-by-step to a hard result (Liquid Glass letterforms).
> These are the rules our Director sub-agent runs. Source doc:
> `data/research/glass-type-postmortem.md`

---

## The core finding

> "Every magnitude in the final file — displacement scales, rim offsets,
> ribbon heights, shadow opacity — was set by looking, not by reasoning."

A text-only agent cannot produce this class of output. The render→look→
critique loop is not an optimisation; it is the mechanism.

Second finding: the canonical recipe from training data was **100% wrong
for the target engine**, and failed *silently*. One-shot tools ship dead
code confidently. A looking agent catches it in one iteration.

---

## 1. Before the first line of code

- **Detect the environment.** Engine, renderer, font availability. The
  right architecture depends on the answer, not on the remembered recipe.
  (`backdrop-filter: url(#svgFilter)` is Chromium-only and is dropped
  silently by Gecko/WebKit — no error.)
- **Write falsifiable acceptance criteria per feature.** Not "looks
  good" — kill-tests. Example: *delete the background; the glass must
  vanish. If it doesn't, it's a painted fill.*
- **Specify the background from the effect's requirements first,
  aesthetics second.** An effect that transforms a backdrop is only
  perceptible where the backdrop carries detail at the effect's own
  spatial scale. Decide displacement amplitude, then place detail at
  that wavelength.

## 2. Build order (never skip ahead)

1. Geometry only — plain flat fill. Confirm size, position, and that
   clips/masks resolve.
2. Then stack the material back-to-front, **screenshotting after every
   layer.**
3. Kill-tests: toggle each layer off individually. No visible change =
   that layer is inert. Find out why.
4. Test aspect ratios (16:9, 1:1, 9:19.5). Cropping bugs are invisible
   at the authoring size.
5. Time a frame. Over ~30ms → look at filter regions first.

## 3. Director owns the tooling, not the coding model

~⅓ of the observed iterations were burned on tooling, not design:
- **Assert the DOM matches the source before diagnosing anything.** Two
  rounds of reasoning were spent on code that had already been deleted.
- **Use real pixel capture.** DOM-reproduction screenshotting
  (html-to-image) doesn't render `backdrop-filter` and mishandles masks —
  the camera lied for two iterations.

Our Director handles both, so the coding model never spends turns here.

## 4. The "made of X" decomposition (generalises to any theme)

> "'Made of X' means the shape becomes an aperture onto a transformed
> instance of X. The glyph contributes only geometry — clip, mask, alpha
> source. It never contributes a fill."

Decomposes identically for *letters made of water*, *a logo in brushed
steel*, *a chart made of paper*: one clip from the shape, one instance of
the material's source, one transform between them, plus a lighting model
at the boundary.

## 5. Other transferable principles

- **Thickness is asymmetry, not outline.** A symmetric rim reads as a
  cut-out hole or as neon. Strong incident rim + weak return light on the
  opposite face + interior falloff = the brain infers volume.
- **Verify magnitudes, never reason them.** Opacities that look sane in
  code are routinely below perceptual threshold against a bright field.
- **Silent spec failures are the expensive ones.** Invalid constructs
  that render *something* wrong are worse than errors.

## 6. What one-shot gets right (don't over-correct)

Composition, the decision to build the material as a layer stack, and the
general shape of the filter chains were right on attempt one. **The
architecture was sound; everything quantitative and everything
engine-dependent was wrong.**

Implication for our product: the agent's job is not to replace the coding
model's design instinct. It is to supply the loop — environment truth,
measurement, kill-tests, and perceptual calibration.
