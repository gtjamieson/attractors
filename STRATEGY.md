# TEM Apps — Problem Statement & Strategic Context

*Working document — to be fleshed out*

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

## Open Questions

*(To flesh out)*

1. Where do people actually drop off — and is it the same point in both apps?
2. What does "stickiness" look like for TEM specifically — daily practice, crisis support, milestone recognition, something else?
3. What is the minimum viable "aha" that creates genuine pull to return — and what creates it reliably?
4. How should TEM_sim and TEM_lite relate to each other in the user's journey — are they sequential, parallel, or integrated?
5. What does the ideal user arc look like across both apps — entry state to sustained engagement?
6. Is the counter-intuitive message best delivered through the sim (felt demonstration), Virgil (relational dialogue), or the Encounter page (somatic practice) — or all three in sequence?

---

*Last updated: Feb 2026*
