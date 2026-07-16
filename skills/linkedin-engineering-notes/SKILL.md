---
name: linkedin-engineering-notes
description: "Mine engineering sessions → LinkedIn drafts. Formats: Engineering Note, Concept Refinement, Architecture Sketch, Design Tradeoff, Research Log, Engineering Investigation."
voice:
  person: "I" # не "we"
  brand: "AI-native R&D engineer. Personal research journal, not company blog."
  tone: "Инженер-исследователь, который столкнулся с проблемой, создал решение для себя и делится находкой. Не ментор, не 'я придумал правильную модель'. Показывать эволюцию мышления: 'я бился в стену → я разделил две вещи → вот что изменилось → я ещё не закончил'. Конкретные примеры из универсальных ситуаций (code review, research), не из внутреннего scaffolding."
  anti_mentor_rules:
    - "Примеры — универсальные (code review, research agent), не domain-specific (Gaming DWH)"
    - "Показывать путь к решению, а не декларировать решение"
    - "Заканчивать честным 'где я сейчас' — что ещё не работает, что исследуется"
    - "Фреймы демонстрировать через механику разделения, не через содержимое"
constraints:
  - "No scaffolding leaks — speak industry language, not internal tooling names"
  - "No framework/library names unless essential to the insight"
  - "Show engineering thinking, not finished products"
  - "Less declaration, more hypothesis + observation + conclusion"
formats:
  engineering-note:
    stars: 5
    trigger: "architectural shift or anti-pattern discovery"
    structure: "Hook → claim → context → experiment/observation → implication"
  concept-refinement:
    stars: 5
    trigger: "new term or conceptual distinction from practice"
    structure: "Old model → new model → why the distinction matters → shift statement"
  architecture-sketch:
    stars: 5
    trigger: "new model/schema (e.g. Professional Frame → Operational Frame → Workspace)"
    structure: "ASCII diagram + textual layer-by-layer explanation"
  design-tradeoff:
    stars: 4
    trigger: "decision to remove X in favor of Y"
    structure: "What removed → why → what gained"
  research-log:
    stars: 5
    trigger: "hypothesis + experiment + observation"
    structure: "Hypothesis / Experiment / Observation / Conclusion"
  engineering-investigation:
    stars: 5
    trigger: "deep dive into a single question"
    structure: "Question → Approach → Findings → Open questions"
upstream: "narrative-shaping"
upstream_contract:
  narrative: "narrative-shaping"
  tension_source: "tension-mining"
  input: "narrative blueprint: Research Identity + Narrative Spine + Artifacts Used + Narrative Form + Key Quotes"
  index: "references/INDEX.yaml (in tension-mining)"
  flow: "tension-mining → narrative-shaping → linkedin-engineering-notes (channel projection)"
pipeline:
  - "1. Load tension file from research-tension-compiler"
  - "2. Pass Draft Gate (mandatory pre-flight checklist — see Draft Gate section)"
  - "3. Identify format from tension structure"
  - "4. Draft post: opening = observation or contradiction, NEVER current_model"
  - "5. Review gate: user approves/edits/rejects"
anti_patterns:
  - "How to build X in 5 minutes"
  - "Top 10 tricks"
  - "Prompt engineering tips"
  - "Tutorial-style content"
  - "Tool/framework announcements"
  - "Scaffolding/internal tool names leaking to audience"
  - "Opening with Current Model instead of Contradiction"
  - "Presenting model as finished framework"
  - "Hiding terminology corrections"
series_title: "AI Engineering Notes"
numbering: "#001, #002, ..."
---

# LinkedIn Engineering Notes — Pipeline

## What This Is

A content pipeline that mines engineering sessions for architectural insights and drafts LinkedIn posts in one of 6 formats.

## Voice

- **Person:** "I" — personal R&D journal, not company blog
- **Brand:** AI-native R&D across domains (DWH, agent architecture, knowledge systems, cognitive engineering)
- **Style:** Hypothesis-driven. Show thinking, not just results. "I observed X → I hypothesized Y → experiment showed Z" > "X is obsolete."

## Formats (6)

Trigger detection is the key. Each format has a specific pattern that signals it.

### Engineering Note ⭐⭐⭐⭐⭐
**Trigger:** architectural shift or anti-pattern discovery
**Structure:** Hook → claim → context → experiment/observation → implication
**Example:** "Why I stopped designing AI agents as procedural pipelines"

### Concept Refinement ⭐⭐⭐⭐⭐
**Trigger:** new term or conceptual distinction from practice
**Structure:** Old model → new model → why the distinction matters → shift statement
**Example:** "Professional Frame vs Operational Frame"

### Architecture Sketch ⭐⭐⭐⭐⭐
**Trigger:** new model/schema
**Structure:** ASCII diagram + layer-by-layer explanation
**Example:** "Professional Frame → Operational Frame → Workspace → Reasoning"

### Design Tradeoff ⭐⭐⭐⭐
**Trigger:** decision to remove X in favor of Y
**Structure:** What removed → why → what gained
**Example:** "Why I removed 100% of capabilities from the skill file"

### Research Log ⭐⭐⭐⭐⭐
**Trigger:** hypothesis + experiment + observation
**Structure:** Hypothesis / Experiment / Observation / Conclusion
**Example:** "Can a filesystem become a native DWH for LLM agents?"

### Engineering Investigation ⭐⭐⭐⭐⭐
**Trigger:** deep dive into a single question
**Structure:** Question → Approach → Findings → Open questions
**Example:** "Decision-Centric Architecture: replacing spec cards with authorized decisions"

## Draft Gate (P0 — enforced, not optional)

Before writing the first sentence of any post, pass this gate. This is an architectural contract, not a guideline.

```
Draft Gate — mandatory pre-flight

□ Load the tension file from research-tension-compiler
□ Read voice_constraints from tension file
□ Read anti_patterns_for_draft / do_not_in_draft from tension file
□ Identify the contradiction (not the current_model) as the post's spine

Opening check:
  □ First paragraph starts with observation OR contradiction
  □ First paragraph does NOT start with current_model

Post structure check:
  □ Current model is introduced as "the model that currently fits observations best" — not as finished truth
  □ At least one artifact (analogy, anti_pattern, etc.) is used to ground the abstraction
  □ Uncertainty is preserved — if tension status is "exploring", the post says so
  □ Terminology corrections from research_progress are visible, not hidden

Voice check:
  □ Researcher tone (not mentor, not preacher)
  □ "I" voice throughout
  □ No scaffolding names leaked
  □ No internal shorthand without explanation
```

If any box is unchecked, fix the draft. Do not proceed to publishing.

## Constraints

1. **No scaffolding.** Internal tool names (Minerva, Hermes, skill_view) stay out. Use industry terms: "data warehouse", "agent runtime", "cognitive environment".
2. **No frameworks.** Unless the framework IS the insight — and even then, only if widely known.
3. **Show work.** "We replaced X with Y and observed Z" > "X is obsolete."
4. **Calibrate confidence.** Hypothesis ≠ finding. Observation ≠ law.

## Anti-patterns (never publish these)
- How-to tutorials
- Tool/framework listicles
- Prompt engineering tricks
- "I built an AI app" — show architectural thinking, not products
