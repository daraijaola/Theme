# Liquid Glass — the round that proved the thesis

This chain is the strongest evidence we have that the product works.
Same model, same capability throughout. The only variable is **whether
it was guided through a render → look → critique loop.**

## The chain

| File | State | What happened |
|---|---|---|
| `01-failed-attempt.html` | ❌ bad | Built from written specs without ever studying how the material *looks*. Too milky, blur far too heavy (14px), weak edges, background too plain for refraction to register, layout evenly spaced with no hierarchy. |
| `02-corrected.html` | ✅ good | After visual research. Lens not fog: 2.5px blur, thin tint, near-transparent centre, bright bevel rim + edge refraction. iOS 26 "Sky" background with real spatial frequency. Glass floats small on the navigation layer. One drop shadow, brutal type contrast. |
| `03-oneshot-weather.html` | ❌ baseline | **One-shot.** Applied the canonical recipe uniformly and stopped. |
| `04-iterated-glass-type.html` | ✅ good | **Same model, guided step by step.** Abandoned the canonical recipe entirely and built a custom optical pipeline from filter primitives. |
| `05-sdf-lensing.html` | ✅ best | The model read its own post-mortem, identified its biggest remaining fault, and fixed it — replacing procedural noise with a generated displacement map. |

## The measurement (03 vs 04)

Counted directly from the source files:

| | `03-oneshot` | `04-iterated` |
|---|---|---|
| `backdrop-filter` | **28** | **0** |
| inset box-shadows | 28 | 0 |
| `feComposite` | 0 | **24** |
| `feGaussianBlur` | 0 | **18** |
| `feFlood` | 0 | **12** |
| `feOffset` | 0 | **8** |
| `feDisplacementMap` | 2 | **8** |
| `feColorMatrix` | 0 | 6 |

One-shot reached for the **formula** and applied it 28 times. The guided
run **constructed the material from physics primitives.** Same model.
That gap is the product.

## The self-correction (04 → 05)

| | `04` | `05` |
|---|---|---|
| `feTurbulence` | 4 | **0** |
| `feImage` | 0 | **2** |

Its own post-mortem said:

> "The refraction is not physically derived. feTurbulence gives an
> organic warp of roughly uniform magnitude across the whole letter
> interior. Real lensing is edge-concentrated — magnitude near zero in
> the middle, rising sharply at the contour, direction along the surface
> normal. That requires an SDF-derived normal map… The current version
> bends the background; it does not lens it. This is the biggest
> remaining gap."

`05` closes exactly that gap: turbulence removed, a generated
displacement map loaded via `feImage`. Visible in the render — ribbons
crossing a stroke are offset where they enter it, strongest near the
contours and near-zero through the counters. Optical profile, not warp.

**`04 → 05` is a self-critique pair** — the model naming its own fault
and fixing it. Rarer and more valuable than human-critique pairs, and
the exact behaviour our Director agent must reproduce.

## Also in this round

- `data/protocol/director-protocol.md` — the operating rules for the
  Director sub-agent, extracted from the coding model's post-mortem.
  Covers environment detection, kill-tests, build order, and the finding
  that ~⅓ of iterations were lost to tooling (so the Director must own
  screenshot and DOM verification).
- `data/prompts/master-theme-prompt.md` — the reusable theme prompt.

## Still to paste in from the source chat

- `data/research/glass-type-postmortem.md` — **the most valuable
  document we have.** The coding model's own post-mortem: why the
  canonical recipe was wrong for the target engine, attempt-by-attempt
  failure analysis, transferable principles, what one-shot structurally
  skips, a cold-start checklist, a trap list, and its own remaining
  faults.
- `data/research/css-scene-craft.md`
- `data/research/liquid-glass-spec.md`
- `data/research/liquid-glass-visual-truth.md`
