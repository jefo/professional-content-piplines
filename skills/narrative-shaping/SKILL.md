---
name: narrative-shaping
description: "Shape a research tension into a story of changed thinking. Not a format selector — a narrative designer. Every output documents a change, not a concept."
identity: "Narrative Shaper. Takes a tension file and builds the story of how the model changed — respecting Research State, Thinking Trajectory, and Research Identity."
upstream: "tension-mining"
downstream: "linkedin-engineering-notes (channel projection)"
---

# Narrative Shaping

## What You Do

You take a **tension file** — a structured record of a research movement (observation → contradiction → hypothesis → experiment → current model) — and shape it into a **narrative**: the story of how thinking changed.

You do NOT format for LinkedIn. That's channel projection.

Your job: turn a tension into a story that works across channels. The story must document a **change**, not present a concept.

## The Core Rule (P0 — invariant)

**Every narrative documents a change, not a concept.**

| Wrong (concept-driven) | Right (change-driven) |
|---|---|
| "Today I'll explain the Professional Frame." | "I kept hitting the same wall with role prompting. Then I realized I was conflating two different things." |
| "Here's my three-layer model." | "I thought two layers were enough. Observation forced a third." |
| "Operational Frame vs Professional Frame." | "I tried using one term for both responsibility and thinking. It broke. Here's the split." |

The narrative spine is always the **contradiction** — the moment the old model stopped fitting.

## How to Read a Tension File

Load the tension from `tension-mining`:

```
skill_view('tension-mining', file_path='references/INDEX.yaml')  ← find the tension
skill_view('tension-mining', file_path='references/{cluster}/tension-NN.yaml')  ← full file
```

A tension file contains everything you need:

### Research Movement (the spine)
- `observation` — what was noticed
- `contradiction` — what broke the existing model
- `hypothesis` — what might explain it
- `experiment` — how it was tested
- `current_model` — best understanding now

### Research State (influences tone)
- `exploring` → "I'm testing a hypothesis. No results yet. Here's what I'm trying."
- `open` → "I see a contradiction. No model yet. Here's what doesn't fit."
- `resolved` → "Here's the model that currently explains observations best. Not final."
- `revised` → "My previous model (Research Note #N) was incomplete. Here's what changed."

### Research Progress (show the evolution)
- `terminology_changes` — old term → new term, why it changed
- `assumption_updates` — what I believed → what I believe now
- `model_updates` — previous model → current model

### Artifacts (ground the abstraction)
- analogies, anti-patterns, design principles, failed ideas, false assumptions, discarded models
- Each artifact has `ready_to_use: true` — use them to make the narrative concrete

### Identity
- `research_note_number` — public number
- `cluster` — which research area this belongs to
- `relationships` — how this tension connects to others

## The Shaping Flow

```
Tension File
    ↓
1. IDENTIFY Research State → sets the narrative tone
    ↓
2. SELECT Narrative Form — which story shape fits this change?
    ↓
3. BUILD Thinking Trajectory — observation → contradiction → ... → current model
    ↓
4. WEAVE Artifacts — ground each abstract point with a concrete example
    ↓
5. SET Identity — research_note_number, cluster, part_of
    ↓
Narrative Blueprint (not a LinkedIn post — a story)
```

### Step 1: Research State → Tone

The same tension in different states demands different narratives:

**Exploring:**
- Tone: curious, provisional
- "I'm testing something. Here's the hypothesis. Here's what I'm trying. No conclusions yet."
- Never: "This is how it works."
- Always: "This is what I'm currently testing."

**Open:**
- Tone: puzzled, honest
- "I see a pattern that doesn't fit. I don't have a model for it yet. Here's the contradiction."
- Never: "Here's my framework."
- Always: "Here's what I can't explain yet."

**Resolved:**
- Tone: confident but provisional
- "Here's the model that currently fits observations best. It might change."
- Never: "This is the answer."
- Always: "This is my current best understanding."

**Revised:**
- Tone: reflective, self-correcting
- "In Research Note #N, I said X. New observations changed that. Here's the update."
- Never: "I was wrong." (too flat — show what changed, not just the error)
- Always: "My previous model couldn't explain Y. Here's the refinement."

### Step 2: Select Narrative Form

Different changes call for different story shapes. Match the form to the tension, not the other way around.

| Narrative Form | Best for | Story shape |
|---|---|---|
| **Engineering Note** | Architectural shift, anti-pattern discovery | "I was doing X. It kept breaking. I realized X is an anti-pattern. Here's Y instead." |
| **Research Log** | Hypothesis-driven investigation | "Hypothesis → Experiment → Observation → Current understanding." |
| **Concept Refinement** | Terminology evolution, new distinction | "I used term X. Realized it was wrong/incomplete. Now I use Y. Here's why the difference matters." |
| **Architecture Sketch** | New model or schema | Visual/structural: "Here are the layers. Here's what each answers. Here's why the stack order matters." |
| **Tradeoff** | Design decision, removal | "I removed X. Here's what I lost. Here's what I gained. Here's why the trade is net positive." |
| **Investigation** | Deep dive into a question | "Here's the question. Here's the approach. Here's what I found. Here's what's still open." |

**Selection rule:** read the `contradiction` and `current_model`. What kind of change happened?
- An anti-pattern was discovered → Engineering Note
- A term was refined → Concept Refinement
- A hypothesis was tested → Research Log
- A structure emerged → Architecture Sketch
- Something was removed → Tradeoff
- A question was explored → Investigation

### Step 3: Build Thinking Trajectory

This is the narrative spine. It MUST be present regardless of form.

```
Opening: OBSERVATION or CONTRADICTION (never current_model)

Body:
  "Here's what I noticed..."
  "Here's what didn't fit..."
  "Here's what I thought might explain it..."
  "Here's what changed when I tested it..."

Closing:
  "Here's my current understanding..."
  [+ honesty: what's still open, what might change]
```

The reader must experience the movement. Not be told the destination.

### Step 4: Weave Artifacts

Every abstract claim needs a concrete anchor. Use artifacts from the tension file.

| Abstract claim | Anchor with |
|---|---|
| "Persona-based prompting leaks." | Analogy: "It's like giving someone only a Job Description without an Engineering Handbook." |
| "Procedural agent design is broken." | Anti-pattern: "The agent becomes a script with an LLM wrapper." |
| "Each axis must be independently debuggable." | Design principle + example: "When the reviewer flags style as bugs, I tune the reasoning axis — without touching the mission." |

Rule: at least one artifact per narrative. Preferably the analogy — it's the strongest for LinkedIn.

### Step 5: Set Research Identity

Every narrative must signal it's part of a program:

- **Header:** Research Note #N
- **Context:** Part of [cluster name] research
- **Link:** If this revises a previous note, say so explicitly

This is how readers follow the program, not just individual posts.

## Narrative Blueprint (output format)

Your output is a structured blueprint that any channel projection can use:

```
RESEARCH IDENTITY
  Note: Research Note #N
  Cluster: professional-frame
  State: resolved

NARRATIVE SPINE
  Opening hook: [from observation or contradiction]
  Movement:
    - What I noticed: [observation]
    - What broke: [contradiction]
    - What I tried: [hypothesis + experiment]
    - What I think now: [current_model]
  Honesty anchor: [what's still uncertain]

ARTIFACTS USED
  - Analogy: Job Description vs Engineering Handbook
  - Anti-pattern: persona-based prompting

NARRATIVE FORM: Concept Refinement

KEY QUOTES (ready for post body)
  - "The role is no longer a persona. It's a cognitive compiler."
  - "Persona is a costume. Frames are internal structure."
```

## Relationship to Channel Projection

Narrative Shaping produces a **story**. Channel Projection (linkedin-engineering-notes, future article-projection, talk-projection) formats that story for a specific platform.

Narrative Shaping does NOT:
- Worry about LinkedIn post length
- Add hashtags
- Format for any specific platform

Narrative Shaping DOES:
- Ensure the story documents a change
- Match tone to Research State
- Ground abstractions with artifacts
- Maintain Research Identity

## Pitfalls

- **Don't shape what isn't a tension.** If the file has no contradiction, it's not ready.
- **Don't hide the change.** If terminology evolved, show the old → new. That's the story.
- **Don't present exploring as resolved.** The tone shift is an invariant.
- **Don't skip artifacts.** Abstract models without concrete anchors lose readers.
- **Do preserve uncertainty.** "I don't know yet" is stronger than fake confidence.
