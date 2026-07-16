# Professional Content Pipelines

Монорепо скиллов для производства исследовательского контента.

## Скиллы

### `research-tension-compiler`
Упаковывает сырые исследовательские сессии в structured tension files — семантический склад мяса.

**Единица:** tension (observation → contradiction → hypothesis → experiment → current model).  
**Выход:** YAML tension file с артефактами (analogy, anti_pattern, design_principle, etc).

### `linkedin-engineering-notes`
Читает tension files из compiler → производит draft LinkedIn-постов в 6 форматах.

**Форматы:** Engineering Note, Concept Refinement, Architecture Sketch, Design Tradeoff, Research Log, Engineering Investigation.  
**Голос:** инженер-исследователь, "I", не ментор.

## Структура

```
skills/
├── research-tension-compiler/       ← upstream: сырьё → tension files
│   ├── SKILL.md
│   └── references/inventory/
│       ├── INDEX.yaml               ← карта всех tensions
│       └── {cluster}/
│           └── tension-NN.yaml      ← один tension
└── linkedin-engineering-notes/      ← downstream: tension → пост
    └── SKILL.md
```

## Интеграция с Hermes

В `config.yaml`:

```yaml
external_dirs:
  - /root/projects/professional-content-pipelines/skills
```
