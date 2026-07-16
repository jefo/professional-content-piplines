# ADR-001: Narrative Architecture — разделение ответственностей

**Status:** accepted
**Date:** 2026-07-15

## Context

Скилл `linkedin-engineering-notes` пытается выполнять две работы одновременно:
- Выбирать историю для tension (narrative shaping)
- Форматировать историю под LinkedIn (channel projection)

Из-за этого pipeline перевёрнут: формат выбирается до истории, стадия исследования не влияет на тон, посты — атомарные единицы без связи с программой.

После появления `research-tension-compiler` (tension mining) стало очевидно разделение слоёв.

## Decision

Разделяем производство контента на три слоя, каждый — независимый skill:

```
Engineering Session
        ↓
  tension-mining         ← бывший research-tension-compiler
  (извлекает tension, наблюдения, гипотезы, терминологические изменения)
        ↓
  narrative-shaping      ← новая ответственность
  (tension → история изменения мышления)
        ↓
  channel-projection     ← LinkedIn / статья / доклад / видео
  (история → платформенный формат)
```

### Терминология (LLM-native, не процедурная)

| Старое | Новое | Почему |
|--------|-------|--------|
| Compiler | Mining | Compiler — процедурная метафора. Mining — обнаружение, не производство. |
| Formats (6) / Trigger Detection | Narrative Shaping | Формат вторичен. Первично — какую историю рассказывает tension. |
| Pipeline | Flow | Pipeline — конвейер. Flow — естественное движение. |

### Принципы narrative shaping

1. **Every post documents a change, not a concept.** Не «Professional Frame», а «я думал X, но наблюдения заставили перейти к Y».

2. **Research State влияет на тон:**
   - `exploring` → «я проверяю гипотезу, результатов пока нет»
   - `open` → «вот противоречие, которое я вижу, но модели ещё нет»
   - `resolved` → «вот модель, которая сейчас лучше всего объясняет наблюдения»
   - `revised` → «моя предыдущая модель была неполной — вот что изменилось»

3. **Research Identity — сквозная:**
   - Каждый пост: Research Note #N, часть кластера X
   - Читатель следит за программой, не за отдельными постами

4. **Thinking Trajectory — архитектура, не пожелание:**
   - Observation → Contradiction → Hypothesis → Experiment → Current Model
   - Это структура каждого narrative, независимо от формата

### Две оси вместо «Formats (6)»

**Research State** (вертикаль) × **Narrative Form** (горизонталь):

| State ↓ / Form → | Engineering Note | Research Log | Concept Refinement | Architecture Sketch | Tradeoff | Investigation |
|---|---|---|---|---|---|---|
| Exploring | ✓ | ✓ | — | — | — | ✓ |
| Open | ✓ | — | ✓ | ✓ | — | ✓ |
| Resolved | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Revised | ✓ | — | ✓ | — | ✓ | — |

Один и тот же tension в статусе `exploring` даёт Research Log. В статусе `resolved` — Engineering Note или Architecture Sketch. Форма выбирается под tension, а не наоборот.

## Consequences

### Что делать сейчас

1. **Переименовать `research-tension-compiler` → `tension-mining`** — mining ближе к «добыче из сессий», не процедурное.
2. **`linkedin-engineering-notes`** — пока оставить как есть (работает), но зафиксировать что он будет разделён на `narrative-shaping` + `linkedin-projection`.
3. **Создать `narrative-shaping`** — новый skill, который принимает tension file и строит историю по Thinking Trajectory, учитывая Research State.

### Будущее

- `linkedin-projection` — форматирует narrative под LinkedIn (длина, хештеги, визуалы)
- `article-projection` — тот же narrative → long-form статья
- `talk-projection` — тот же narrative → структура доклада

Один narrative — много projections.

## Alternatives considered

- **Оставить один skill** — отвергнуто: нарушает single responsibility, pipeline перевёрнут.
- **Compiler как метафора** — отвергнуто: процедурное мышление, противоречит LLM-native архитектуре.
