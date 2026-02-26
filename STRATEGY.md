# TEM Apps — Problem Statement & Strategic Context

*Working document — updated Feb 2026*

---

## The Design Constraint

**TEM must feel different by being more accurate, not more elaborate.**

The world is full of frameworks for people in pain. TEM is different — but layering Buddhist vocabulary, Dantean structure, and attractor physics on top of each other produces more noise, not less. Each layer felt like differentiation during design; together they became the cognitive load that causes users to leave.

What actually cuts through is precision. Not a framework — a recognition. The moment that lands is the one that names exactly what the person is experiencing right now, in a way they've never heard named before.

The attractor sim already does this once: clicking "good choice / bad choice" and getting the same outcome. That moment doesn't need the vocabulary around it. It lands because it's true and the user has lived it.

**The governing design question for every page, every interaction, every line of copy:**

> *What is the single most precise thing TEM can show this person — before they've had to learn anything — that makes them think: "that's me, and I've never seen it named like that before"?*

If an element doesn't serve that question, it is cognitive load, not content.

**Corollary:** Both apps have suffered from being designed to demonstrate the intelligence of the model rather than to serve the user's actual need. The user's need is recognition, not education. These require different design choices. Education feels more impressive to build. Recognition is harder and rarer.

---

## The Core Problem

Both apps exist. People are drawn to them. They don't keep using them.

The stickiness problem is not a technical failure — it is a consequence of the counter-intuitive nature of TEM's central message. The person who opens either app arrives in a goal-oriented state: *I want to fix X*. That orientation — wilful, attainment-seeking — is precisely what TEM identifies as the structural source of the problem. The app must simultaneously meet people where they are and invert the frame they arrived with, without triggering the defensive reaction that premature inversion causes.

This is the paradox at the heart of the design challenge:

- Do it too fast → feels dismissive, user leaves
- Never do it → the app becomes another cognitive self-help tool that feels useful but produces no lasting change
- Do it well → a genuine shift occurs, and the user has a reason to return

The current apps have not yet reliably produced that shift at scale.

---

## TEM — Analysis

### The Central Insight

Most approaches to personal change assume that the right knowledge, motivation, or technique applied with sufficient effort will produce lasting results. TEM's claim is that this is structurally wrong — not because people fail to try hard enough, but because willful effort operates at the wrong level of the system.

Behaviour is governed by the shape of the underlying terrain, not by the position of the ball on it. Choices — good or bad — move the ball temporarily. The terrain pulls it back. Lasting change requires reshaping the terrain itself. That cannot be done by pushing harder.

### The Model

The attractor landscape provides a precise vocabulary for this:

- **Fear** is a repeller — the system naturally moves away from it, and the system becomes unstable when fear dominates
- **Desire** is an attractor — the system is drawn toward it, stabilising around it
- **Doing** is the visible surface behaviour — choices, actions, effort — which appears to be the lever of change but is actually constrained by the Fear/Desire balance underneath
- The **curve** — shaped by the competitive balance between Fear and Desire — is what determines long-term behaviour, not individual choices

Key corollaries:
- Increased fear causes desire to become shallow and superficial (the concave bubble — expansion without depth)
- Increased fear makes the system unstable — cause-and-effect thinking creates a vicious cycle
- Good choices and bad choices are structurally equivalent — both are karma insofar as they keep the system in its current attractor state
- Lasting change is not achieved by Doing but by changing the nature of the underlying system

### The Journey (Dantean Map)

| Stage | Dante | TEM |
|-------|-------|-----|
| Entry | Dark Wood | Crisis — presenting problem, ego's failed quick fixes |
| Descent | Hell | Naming the patterns: Attachment → Karma → Samsara |
| Ascent | Purgatory | Active engagement — shifting Fear/Desire balance |
| Handoff | Summit | Virgil (structure/reason) steps back |
| Arrival | Paradise | Beatrice — direct encounter with felt sense / core self |

The shift from **Path of Attainment** to **Path of Acceptance** is the metagame move:
- Path of Attainment: trying to change behaviour from within the same attractor landscape
- Path of Acceptance: changing the landscape itself through expanding self-awareness

*"When you no longer fear Fear it ceases to be an obstacle, which changes the structure of the system as a whole."*

### The Metagame

Most people are playing the basic game — chasing outcomes, managing symptoms, trying to outcompete their own resistance. The metagame becomes available when the impossibility of self-grasping is fully accepted. This is not a technique. It is a shift in the level at which the person is operating.

The app's job is to create the conditions for this shift — not to produce it directly.

---

## TEM_sim — Where It Fits

### What It Is

An interactive Ionic app embedding the HTML5 attractor landscape simulation. Structured as a two-act demonstration followed by synthesis:

- **Act 1 — Path of Attainment** (`Cause_effect` → `Attachment`, `Karma`, `Samsara`): the diagnosis — showing how the vicious cycle operates through direct interaction
- **Act 2 — Path of Acceptance** (`New_Change`): the pivot — Fear/Desire as the real levers
- **Synthesis** (`DIY_enlightenment`, `Lifes_metagame`, `TEM`): the full sim and the method

### What It Does Well

- The "Good choices / Bad choices" buttons are a genuine felt inversion of cause-and-effect thinking — morally opposite actions, identical structural outcomes
- The sim is interactive before it is explanatory — the user experiences the model before reading about it
- The two-path structure mirrors the TEM journey: diagnosis before prescription
- The Buddha imagery grounds the model in a tradition that has navigated this terrain

### Where the Gap Is

- The user understands the model and then has nowhere to go. There is no bridge from *"I see how this works in theory"* to *"I see how this applies to my actual Fear/Desire landscape right now"*
- The content is explanatory and conceptual — it does not invite the user into their own experience
- There is no progression, no return loop, no unresolved tension that creates pull to come back
- The "aha" is a one-time intellectual moment, not a recurring felt-sense one

---

## TEM_lite — Where It Fits

### What It Is

An AI-powered guide app. Virgil (Claude Sonnet 4.5 via Cloudflare Worker) meets the user in their specific struggle. The journey:

| Page | Stage | What happens |
|------|-------|-------------|
| Launch | Threshold | Entry, first impression |
| Patterns | Inferno | Conceptual recognition of ego patterns |
| Chat | Purgatorio | Dialogue with Virgil — perspective shift, earning trust |
| Encounter | Beatrice handoff | Felt-sense practice — direct experience |
| Sim | Educational | Attractor landscape embed |
| TEM | Reference | The method explained |

### What It Does Well

- Virgil's voice is relational and personal — meets the user in their actual struggle (`$v.dilemma`)
- The Patterns page names universal ego defenses without diagnosing or moralising
- The Encounter page is designed for the right thing — somatic, not cognitive
- The AI guide embodies the Empty Presence principle: no agenda, no history, no social performance required

### Where the Gap Is

- The journey from Pattern recognition → Chat → Encounter may not be creating enough pull to reach the Encounter page repeatedly
- The Encounter page (where lasting change is seeded) is the hardest destination to reach and the least obvious reason to return to
- Without a sense of progression, the user may not know where they are in the journey or that there is a journey at all
- A single dilemma (`$v.dilemma`) anchors the session, but there is no visible arc across sessions
- The inversion (from "fix X" to "the fixing is the problem") may be happening too late, too fast, or not at all

---

## Architecture Decision — One App

**TEM_lite absorbs the sim. TEM_sim is retired.**

### Rationale

TEM_sim was built around the sim as the hero, surrounded by explanation. But the sim's most powerful moment — good choice / bad choice, same outcome — only lands when the user already has their own struggle in mind. Virgil establishes that struggle first. The correct sequence is:

> Virgil names the dilemma → sim shows the structural reason why effort hasn't worked

In that order, the sim is a revelation. In TEM_sim's order, it is a demonstration looking for a problem to solve.

Two apps also meant two metaphor systems (Buddhist / Dante) with no bridge, double the maintenance, double the drift, and double the cognitive load for any user who encountered both.

The Sim page already exists in TEM_lite. The infrastructure is there. The problem was placement and sequence, not absence.

### What changes

- TEM_sim is retired — no further development
- The Buddhist vocabulary (attachment, karma, samsara) is retired — Dantean framing is the single consistent metaphor system
- TEM_lite becomes the sole app
- The standalone Sim page is retired — the sim is embedded directly into the pages that need it, in the mode that serves each page's specific purpose
- The current TEM_lite page sequence is revised (see Journey Design below)

### Journey Design — Revised Page Sequence

The sim appears twice, in different modes, each doing specific work:

| Page | Stage | Sim | Purpose |
|------|-------|-----|---------|
| Launch | Threshold | — | Entry — met, not redirected |
| Patterns | Inferno | Mode 1 (Karma) — interactive | Visual proof: good choice / bad choice, same outcome. "Here's why the pattern persists regardless of what you do." Interactive is appropriate — clicking both buttons and getting the same result *is* the recognition. |
| Chat | Purgatorio | — | Virgil makes it personal — "this is *your* version of it." Creates the conditions to stop fixing. |
| Encounter | Beatrice handoff | Mode 3 (New_Change) — constrained | Pivot from doing to being. Sim visible but not fully interactive — animating to show Fear decreasing, landscape shifting. "Notice what happens" not "try this." Interactive manipulation would re-engage doing mode. |
| TEM | Reference | — | The method explained |

**Why two modes, not one:**
Mode 1 proves why nothing changes. Mode 3 shows what actually can. That is not repetition — it is a coherent arc told in two visual moments, each serving a different stage of recognition.

**The Encounter design constraint:**
The Encounter page must not present itself as something to do. No instructions, no steps, no technique. Any "how to" language immediately re-engages the doing orientation and the page undermines itself. The form must embody the content — presence invited, not effort directed. Virgil's handoff to Encounter is itself the pivot from doing to being.

### Stickiness

Crisis-driven, not habit-driven. TEM's message is anti-goal-oriented — streaks and milestones are Path of Attainment mechanisms and are wrong for this app. The user returns when the pattern reasserts itself and they know the app is useful in that moment. This requires the first session to produce a real shift, not just an intellectual one. If it does, the user knows where to go next time they're stuck.

### The Minimum Viable "Aha"

Not the sim moment — that's structural recognition, cognitive. The pull that brings people back is: *"I just noticed myself doing the thing while I was doing it."* Real-time pattern recognition at the felt-sense level. That is what the Encounter page exists to produce. Cognitive insights fade. A somatic moment lingers. Encounter is therefore the most important page in the app — and must be the easiest to return to directly.

### Ideal User Arc

> Crisis / stuck ("I want to fix X") → Launch (met, not redirected) → Patterns + sim Mode 1 (recognises the pattern visually — not diagnosed) → Chat (Virgil names their specific version — feels seen) → Encounter + sim Mode 3 (pivot from doing to being — notices Fear directly) → Return at next crisis, knowing where to go

The arc is not linear in practice. But the sequence matters on first use — each step primes the next. On return, the user should be able to go directly to Encounter without repeating the full journey.

### How the Inversion Is Delivered

All three mechanisms, in sequence, each doing different work:

- **Patterns + sim Mode 1** — structural/visual: *"here's the landscape you're living in, and why effort doesn't change it"*
- **Chat / Virgil** — relational: *"this is your specific version of that pattern"* — creates conditions to stop
- **Encounter + sim Mode 3** — somatic: *"this is what Fear actually feels like right now, and what happens when it shifts"*

The inversion does not happen at any single point. It emerges from the sequence. It lands — if it lands — at Encounter. "Fix X" becomes "the fixing is the problem" only when felt, not when understood.

---

*Last updated: Feb 2026 — architecture decision; journey redesigned; open questions resolved*
