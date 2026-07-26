# Experiments — the preference chain

Every file here is dataset material. Nothing gets deleted: the bad
outputs are as valuable as the good ones, because the product is
trained on the *gap* between them.

## disco-ball/ — six rounds, one object

The core lesson chain. Each file is a ❌/✅ pair with the one before it.

| File | State | The critique that forced the next round |
|---|---|---|
| `00-baseline-slop.html` | ❌ bad | Clip-art disco: mirror ball + "boogie". No research. The default failure mode of every model. |
| `01-sphere.html` | better | Real 3D tile sphere, computed lighting. But: no beams, no visible light source, digitally sterile, no film treatment. |
| `02-scene.html` | better | Pinspot, volumetric cone, orbiting spots, grain, halation, follow-through, offset clocks. But: object had no *relationship* to its environment. |
| `03-realism.html` | better | Grounding, bounce light, colour bleed, ambient occlusion, falloff, fresnel, imperfection, depth of field. But: wrongly bathed in orange. |
| `04-relight.html` | better | Colour correction — silver ball, blue/violet/magenta room. Starburst flares. Still looping visibly. |
| `05-definitive.html` | ✅ best | Additive `plus-lighter` light, baked multi-scale bloom, spring-physics pendulum, noise-driven motion, Poisson sparkles, lens-flare system, canvas particle engine. |

**Lesson:** research → critique → name the fault → fix → repeat.
Never "make it better"; always "no follow-through: the cable is rigid
while the ball sways."

## theme-embedding/ — the real product target

`disco-without-disco.html` — a creative-studio landing page with **zero
disco imagery**. The theme lives entirely in design language: chrome
type with irregular sheen sweeps, additive room lighting, Poisson
diffraction glints, attack-fast/decay-slow hovers, offset card clocks,
film grain.

**Lesson:** theme ≠ drawing the theme's object. The agent may design
literal artifacts when it judges right, but theme-as-design-language
is the core skill.

## liquid-glass/ — the failure worth keeping

| File | State | Why |
|---|---|---|
| `01-failed-attempt.html` | ❌ bad | Built from written specs without studying how the material actually *looks*. Too milky, blur too heavy (14px), weak edges, background too plain, layout evenly spaced with no hierarchy. |
| `02-corrected.html` | ✅ good | Lens not fog: 2.5px blur, thin tint, near-clear centre, bright bevel rim + edge refraction. iOS 26 "Sky" background with real frequency to bend. Glass floats small (pill tab bar inset 21px + search island). One drop shadow, brutal type contrast. |

**Lesson:** specs are not sight. Research must include how a thing
*looks*, not only how it's described. This is the highest-value ❌/✅
pair in the repo — the failure and the fix have identical intent.

## data/

- `research/disco.md` — the research-phase output format: cultural
  root, spatial/lighting DNA, graphic DNA, materials, palette,
  motion DNA, **anti-slop guardrails**, reference anchors.
- `vocab/critique-vocabulary.md` — the critique language. Every term
  paired with the sentence that uses it. This teaches the model to
  name faults instead of gesturing at them.

Two further research reports (elite CSS scene-craft; Liquid Glass
visual truth) live in the chat that produced these files — paste them
into `data/research/` when convenient.
