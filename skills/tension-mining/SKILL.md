---
name: tension-mining
description: "Mine research sessions for tensions — the fundamental unit of a research journal. Attention-guide, not procedure: signals of contradiction, terminology shifts, architectural decisions."
identity: "Tension Mining. Discovers research movements in engineering sessions and structures them as tension files."
upstream: null
downstream: "linkedin-engineering-notes (future: narrative-shaping)"
---

# Tension Mining

## What You Do

You read research sessions and extract **tensions** — the fundamental unit of a research journal. A tension is not a concept. A tension is a *movement*: observation → contradiction → hypothesis → experiment → current model.

Your output is a **tension file**: structured YAML that downstream skills consume to shape narratives and produce publications.

## The Core Insight (read this first, every time)

The unit of content is **not a concept.** It is a **resolved tension.**

| Wrong unit | Right unit |
|---|---|
| "Today I'll explain the Professional Frame." | "Today I'll show what contradiction forced me to invent the Professional Frame." |
| Inventory of knowledge | Laboratory journal |
| Here's my model | Here's the model that currently fits observations |

Readers follow researchers, not frameworks. The difference: researchers show the path, including failed hypotheses and terminology corrections.

### Architectural Contract (P0 — invariant)

When drafting a post from a tension file, the opening paragraph **MUST** begin with either:

- **Observation** — what you noticed ("For months I've been observing...")
- **Contradiction** — what didn't fit ("The standard approach says X. But I kept hitting...")

**NEVER** begin with Current Model.

This is not a guideline. This is the invariant that prevents the system from drifting into "Today I'll explain..." content. If a draft begins with the model, reject it and rewrite from the contradiction.

## Target Format: Tension File

```yaml
id: "tension-NN"
title: "Short description of the contradiction resolved"
status: exploring | open | resolved | revised

# ── Path: the research movement ──

observation: >
  What I noticed. Concrete. Observable. Not an interpretation.

contradiction: >
  What didn't fit. The thing that broke the existing model.

hypothesis: >
  What I thought might explain it. Could be wrong — that's fine.

experiment: >
  How I tested it. What changed when I applied the hypothesis.
  Concrete: "before → after" if possible.

current_model: >
  What I believe now. Possibly still provisional.

# ── Research Progress: how the model evolved (P1) ──

research_progress:
  terminology_changes:
    - old: "Methodological Frame"
      new: "Professional Frame"
      reason: "Methodology is only one component. Professional Frame also includes epistemology, heuristics, quality standards, intuition."
      date: 2026-07-11
  assumption_updates:
    - old: "Role + Knowledge is sufficient for specialist agents"
      new: "Two independent axes (Operational + Professional) produce more traceable behavior"
      reason: "Persona leaks across decisions. Independent axes don't."
      date: 2026-07-11
  model_updates:
    - old: "Two-layer model (Operational + Professional)"
      new: "Three-layer model (Workspace → Operational → Professional → LLM)"
      reason: "Missing the knowledge environment as a separate axis"
      date: 2026-07-11

# ── Relationships: knowledge graph of the research program (P2) ──

relationships:
  refines: []        # tension-NN — this tension makes more precise
  extends: []        # tension-NN — this tension adds to
  replaces: []       # tension-NN — this tension supersedes
  contradicts: []    # tension-NN — this tension reverses
  supports: []       # tension-NN — this tension provides evidence for
  derived_from: []   # tension-NN — this tension was inspired by

# ── Artifacts: re-usable building blocks for drafting ──

artifacts:
  - type: analogy
    content: "..."
    ready_to_use: true
  - type: anti_pattern
    content: "..."
    ready_to_use: true
  - type: design_principle
    content: "..."
    ready_to_use: true
  - type: open_question
    content: "..."
    ready_to_use: true
  - type: tradeoff
    content: "..."
    ready_to_use: true
  - type: diagram
    content: "..."  # ASCII diagram or description
    ready_to_use: true
  - type: unexpected_consequence
    content: "..."
    ready_to_use: true
  - type: failed_idea
    content: "An approach that didn't work. Why it failed. What I learned."
    ready_to_use: true
  - type: false_assumption
    content: "Something I believed that turned out incorrect. When I realized. What replaced it."
    ready_to_use: true
  - type: discarded_model
    content: "A model I used and abandoned. Why it stopped fitting observations."
    ready_to_use: true

# ── Public Research Note (P2) ──

research_note_number: null  # assigned when published (e.g., 14). null = not yet published.
research_note_title: null    # the public-facing title ("Research Note #14: ...")

# ── Ready-to-use formulations ──

hooks:
  - "A hook that makes the reader stop scrolling."

key_distinctions:
  - "X is this. Y is that. The difference matters because..."

ready_quotes:
  - "A sentence that works standalone — for the post body or comments."

# ── Series connectivity ──

cluster: "cluster-name"  # tensions belong to thematic clusters
leads_to:
  - "tension-NN"  # what tension this one naturally leads into

# ── Drafting constraints (for downstream skills) ──

voice_constraints:
  - "Researcher, not mentor. 'Here's what I'm observing' not 'Here's what you should do.'"
  - "Show the path, not just the destination."

anti_patterns_for_draft:
  - "Don't present as a finished framework. Present as current best model."
  - "Don't hide terminology corrections — they're research signals."
  - "Don't use internal shorthand (scaffolding names, domain-specific examples)."
```

## How to Mine a Session

When reading a session, you're looking for **research movements.** Here's what to pay attention to — not as a procedure, but as an attention guide:

### Signals of a tension forming

- User says "это не то", "мы пересмотрели", "проблема не в X, а в Y", "оказалось что..."
- Assistant acknowledges: "ты прав", "понял", followed by a shift in architecture
- A term changes: "Methodological Frame → Professional Frame"
- Something is removed: "14 capabilities → 0"
- A new distinction emerges: "это не X, это Y — потому что они отвечают на разные вопросы"

### Signals of artifacts

- An analogy appears: "это как Job Description vs Engineering Handbook"
- An anti-pattern is named: "procedure-based design — ошибка"
- A design principle is stated: "каждая ось должна быть независимо отлаживаема"
- An open question lingers: "сколько правил в Professional Frame — too many?"
- A tradeoff is articulated: "больше осей = больше debuggability, меньше = проще писать"

### Signals of incomplete tensions

- Hypothesis stated but no experiment yet
- Current model exists but user says "это пока гипотеза" or "не уверен окончательно"
- → mark as `status: exploring`, not `resolved`

## Where to Store

```
references/
├── INDEX.yaml              ← map of all tensions: id, title, status, cluster
├── {cluster-name}/
│   ├── tension-01.yaml
│   ├── tension-02.yaml
│   └── ...
```

INDEX.yaml format:
```yaml
clusters:
  professional-frame:
    tensions:
      - id: "tension-01"
        title: "Role+Knowledge is the wrong model"
        status: resolved
      - id: "tension-02"
        title: "Operational vs Professional — two questions"
        status: resolved
      - id: "tension-03"
        title: "Methodological → Professional (terminology)"
        status: exploring
```

## Operating Rhythm

- **During research sessions:** you are in the session. You witness tensions forming. After the session (or when asked), extract them.
- **Weekly planning session:** user asks "что у нас есть на неделю" → scan INDEX.yaml for `resolved` + `exploring` tensions → suggest posting candidates.
- **On new discovery:** user shares a session or insight → extract tension → write file → update INDEX.

## Pitfalls

- **Don't invent tensions that aren't in the session.** A tension is extracted, not created.
- **Don't file every observation as a tension.** Only when there's actual contradiction + movement.
- **Don't mark as resolved without experiment/observation.** If it's still speculative → `exploring`.
- **Do extract artifacts even for exploring tensions.** An analogy might be ready before the model is.
- **Do preserve terminology corrections.** They're research gold — show that you refine, not just declare.
