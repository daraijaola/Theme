# DESIGN CRITIQUE VOCABULARY
> Terms surfaced across iterative research (mirror ball studies 1→4).
> Purpose: dataset material — the critique language our model should learn
> to *name* faults instead of saying "make it better."
> Format: term — what it means — how to use it in a critique.

---

## PASS 1 — SCENE & LIGHT PHYSICS

**Volumetric light** — light made visible as shafts/cones in hazy air. → "There are no visible beams; add volumetric light."

**Pinspot** — the focused spotlight aimed at a mirror ball (classically at ~45°). → "What's lighting this? Show the source."

**Specular vs diffuse** — mirror-sharp reflection (hard hot glints) vs soft scattered glow. → "This surface glows softly; a mirror should glint specularly."

**Kinetic lighting** — theatrical rigs that move/transform (the real Studio 54 signature). → "Lighting is static; it should evolve."

**Halation** — warm red-orange bloom around bright lights, from light bouncing inside film. → "Highlights clip clean; they should bloom warm like 70s film."

**Film grain** — structured organic texture of film (not digital noise); in CSS: SVG turbulence animated with steps(), soft-light blend. → "Too digitally clean; add grain."

**Color grade** — overall tonal treatment (warmth, vignette, S-curve contrast) unifying a frame. → "Colors feel raw/un-graded."

**Bloom** — glow spilling beyond a bright source's edges. → "Bright points are hard-edged; light should spill."

---

## PASS 2 — MOTION CRAFT (Disney's principles, applied)

**Easing (slow-in/slow-out)** — acceleration/deceleration; nothing real moves at constant speed. → "This travels at cruise-control; ease it."

**Follow-through** — parts keep moving after the main body stops; nothing moves as one rigid unit. → "The cable doesn't sway when the ball moves."

**Overlapping action / phase offset** — related parts move on slightly shifted timing. → "Ball and cable are perfectly synced; offset them."

**Arcs** — natural motion follows curves, not straight lines. → "These particles move in straight lines; give them arcs."

**Secondary action** — small supporting motions around the primary one (flicker, shimmer, drift). → "One thing moves and everything else is dead."

**Timing = weight** — heavy things respond slowly, light things quickly. → "This huge ball starts/stops like it's weightless."

**Attack and decay** — how an effect blooms in and fades out (like a musical note). → "The glint snaps on/off like an LED; give it attack/decay."

**Offset clocks** — no two animation layers share a duration; synced loops read as fake. → "Everything repeats on one clock."

**Anticipation** — a small counter-move before the main action.

**Staging** — directing the eye to one clear focal event at a time.

**Exaggeration** — amplifying beyond literal reality so motion reads; pure realism can be dull.

---

## PASS 3 — CGI REALISM (why renders look fake)

**Global illumination (GI)** — light bouncing between surfaces, filling shadows, wrapping corners. → "Shadowed areas are flat black; where's the bounce light?"

**Color bleeding** — bounced light carries the color of what it hit (violet wall tints the ball's dark side). → "Nothing tints anything; surfaces ignore each other."

**Ambient occlusion (AO)** — darkness trapped in crevices, seams, contact points; its absence is a classic fake-tell. → "Tile grooves have no trapped shadow."

**Contact shadow / grounding** — the shadow relationship anchoring an object to its environment; floating objects break realism. → "The ball floats; nothing anchors it to the room."

**Light falloff (inverse-square law)** — brightness dims with distance from the source. → "Far spots are as bright as near ones."

**Fresnel effect** — reflective surfaces reflect more at grazing angles; spheres get a bright rim at the silhouette. → "The ball's edge should catch a rim of light."

**Imperfection principle** — no real surface is flawless; scratches, dust, dead tiles, uneven rows sell realism; uniformity smells fake. → "All 300 tiles are identical; kill a few."

**Environment reflection** — glossy objects mirror their surroundings, not just the light source. → "The ball reflects nothing of the room it's in."

**Depth of field (DOF)** — a lens focuses at one distance; near/far things soften. → "Everything is equally sharp; no lens would do that."

**Chromatic aberration** — subtle color fringing on high-contrast edges from a lens. → (use sparingly) "Hottest highlights could fringe."

**Motion blur** — fast-moving things streak on camera.

**Shadow terminator** — the soft gradient where light rolls into shadow on a curved surface; hard terminators look CG.

**Soft vs hard shadows** — big/close light sources make soft shadows; small/far make hard theatrical ones. → "Shadow edge quality doesn't match the light source."

**HDRI / area light (concepts)** — lighting a scene with a captured real-world environment / surface-sized emitters; the reference standard for believable light.

---

## THE MASTER PATTERN

A scene feels real when it has, in order of importance:
1. **Relationships** — objects ground, occlude, tint, and reflect each other (GI, AO, contact, bleed, environment reflection)
2. **Physical light law** — falloff, fresnel, specular behavior, soft/hard logic
3. **Imperfection** — controlled flaws everywhere
4. **A lens** — grain, halation, bloom, DOF, grade: the frame was *photographed*, not drawn
5. **Motion grammar** — easing, arcs, follow-through, offsets, weight

Critique formula: name the missing term + point at the evidence + state the fix.
"No follow-through: the cable is rigid while the ball sways — let it lag on an offset phase."
