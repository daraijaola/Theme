# Theme — Project Context

Read this at the start of every session. This is a briefing, not a task list.
As of this writing the project is in the **planning phase** — no implementation
exists yet. Do not start building unless explicitly asked.

## What we're making

An **MCP server that coding agents connect to** (Claude Code, Codex, Cursor).

A user gives a theme — e.g. "disco" — and our system guides the coding agent,
step by step, into producing a **unique, heavily-themed, detailed frontend**
(HTML/CSS), instead of the generic designs these models produce by default.

The generic-output problem is the whole product. Anyone can ask a coding agent
for a "disco landing page" and get purple gradients and a mirror-ball emoji.
We exist to make the output specific, committed, and detailed.

## Core architectural fact

**We do not generate the frontend. The coding agent does.**

We are the director in the loop. Our own model — a fine-tuned open-source
**Qwen** — converses with the coding agent turn by turn, steering it toward a
distinctive result.

- **Transport:** MCP. Not API calls. One integration per coding app to start;
  a universal connector is the long-term goal.
- **Structure:** a main agent orchestrating **sub-agents**, each owning a
  different aspect of the theme.
- **Latency is a non-constraint.** 30 minutes is fine if the result lands at
  ~99% satisfaction. This buys us many turns, deep sub-agent passes, and
  self-critique loops — spend the time.

## Economics

Users connect **their own** Claude Code / Codex subscription, so their plan
pays for the generation tokens. Our cost is Qwen inference only.

Bootstrapped. No funding.

## Training approach

Preference-style, **DPO-like**.

The important half is the **rejected** side: we penalize generic output, not
just reward good output.

Dataset shape: `theme → (generic ❌, distinctive ✅)` pairs.

## Repo map

- **`data/research/`** — theme DNA research, one file per theme. Cultural root,
  spatial/lighting DNA, graphic DNA, materials, palette, motion DNA, anti-slop
  guardrails, reference anchors. This is the research-phase output format.
- **`data/vocab/`** — critique language. Terms paired with the sentence that
  uses them, so the model names a fault instead of gesturing at it.
- **`experiments/`** — preference chains: bad → good outputs on the same brief.
  The ❌ files are dataset material, not clutter. **Never delete, rename, or
  tidy them** — the product is trained on the gap between the pair. See
  `experiments/README.md` for what each file is and the lesson it encodes.

## Team

| Who | Role |
| --- | --- |
| Owner (repo author) | Direction, product |
| Tech Blaze | Building |
| Henry | Research |
| Deji | UGC ad for launch |

## Go-to-market

Ship → go viral via the launch ad → target **$10–20k**.

## Open questions to resolve in planning

These are flagged, not decided. Don't treat them as settled.

1. **"Generic" needs an operational definition before the dataset exists.**
   DPO trained on vibes produces a model that penalizes vibes. Whatever we
   write down as eval criteria becomes the training label in practice — so
   **eval criteria likely come before the dataset plan**, not after.

2. **MCP is a tool protocol, not a conversation channel.** The agent calls us;
   we cannot call it. "Step-by-step conversing" has to be constructed out of
   tool-call turns the agent chooses to make — which means our **tool
   descriptions and return payloads** are the mechanism that keeps it in the
   loop. This needs pinning down in the architecture doc.

## Planning agenda (next session)

- v1 scope
- Architecture doc
- Dataset plan
- Eval criteria
