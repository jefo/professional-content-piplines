# AI Systems Research Notes

## Fundamental Question

**What constitutes competence in an AI agent?**

Not "how to prompt better." Not "how to build agents." But: what is the architecture of professional competence — and how do you give it to an LLM?

This research program investigates the structure of specialist thinking: how to decompose "being an expert" into components that can be independently designed, debuggable, and composable.

## Why This Exists

Most AI content discusses models, tools, frameworks, or prompts. This program operates one level above: the engineering of *professional cognition* for AI systems.

The object of study is not the agent or the LLM. It is the structure of competence, decision-making, and knowledge organization.

## Production Architecture

Research output flows through three layers:

```
Engineering Session
        ↓
  tension-mining           ← extracts tensions, observations, hypotheses
        ↓
  narrative-shaping        ← shapes tension into a story of changed thinking
        ↓
  channel-projection       ← formats story for LinkedIn / article / talk
```

Each layer is an independent skill in this repository. They are not a pipeline — they are a stack where each layer adds a dimension: structure → story → format.

## Current Research Areas

### Professional Frame Architecture
What replaces "role prompting"? A three-axis coordinate system:
- **Workspace** — what exists (data, tools, ontology)
- **Operational Frame** — what I owe (mission, authority, boundaries)
- **Professional Frame** — how I think (evidence standards, reasoning patterns, quality criteria)

### Contracts vs. Procedures
Why procedure-based agent design (task classifier → strategy catalog → steps) is an architectural anti-pattern — and how architectural contracts replace workflows.

### Knowledge Substrates
Can a filesystem become a native data warehouse for LLM agents? What changes when the DWH is the primary cognitive environment, not just a data source?

### Decision-Centric Architecture
Replacing spec-card pages with pages built around authorized decisions — a model for content that serves reasoning, not information retrieval.

## Research Method

I publish **Research Notes** — not finished frameworks, but the current model that best fits my observations.

Each note documents a **resolved tension**: observation → contradiction → hypothesis → experiment → current model. Failed hypotheses and terminology corrections are part of the record, not hidden.

This is a laboratory journal, not a product announcement.

## Publication Policy

- Research Notes are numbered and sequential
- Each note shows the path, not just the destination
- "I don't know yet" is a valid conclusion
- Terminology corrections are explicit: "I used term X, realized it was wrong, now use Y. Here's why."
- No scaffolding names. No internal shorthand. Industry language only.

## Terminology

Terms are refined as the research progresses. See individual Research Notes for terminology evolution records.

| Term | Status | Definition |
|---|---|---|
| Operational Frame | Stable | What the agent is responsible for: mission, authority, boundaries |
| Professional Frame | Evolving | How the agent thinks: evidence standards, reasoning discipline, quality criteria |
| Workspace | Stable | The knowledge environment: data, tools, ontology |
| Tension | Method | The fundamental unit: observation → contradiction → hypothesis → experiment → current model |

## Open Problems

- How many rules in a Professional Frame is too many? When does reasoning discipline become a straitjacket?
- What happens when Operational Frame and Professional Frame conflict?
- Can Professional Frames be composed? If an agent needs both "data analyst" and "code reviewer" reasoning — merge or layer?
- What is the minimal Professional Frame that still prevents hallucination?

## Research Notes Index

| # | Title | Status | Date |
|---|---|---|---|
| 1 | Your AI agent doesn't need a personality. It needs a coordinate system. | published | 2026-07 |
| 2 | Why I stopped designing AI agents as procedural pipelines | published | 2026-07 |
| — | Terminology: Methodological Frame → Professional Frame | drafting | — |
| — | Four components of Professional Frame | exploring | — |
| — | Filesystem as native DWH for LLM agents | exploring | — |
| — | Decision-Centric Architecture | resolved | — |

---

*This is a living document. Last updated: 2026-07-15.*
