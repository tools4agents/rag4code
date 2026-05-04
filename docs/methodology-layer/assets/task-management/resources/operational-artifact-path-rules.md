# Operational Artifact Path Rules

> Status: Draft  
> Scope: path rules для operational artifacts с initiative workspace и без него  
> Role: focused reference для размещения inputs, tasks and evidence outputs в `operational_scope/`

## Назначение

Этот resource фиксирует правило путей для operational artifacts в новой SDLC-oriented модели.

Цель — единообразно размещать artifacts, связанные с initiative, внутри initiative workspace, а artifacts без initiative — в соответствующих top-level каталогах `operational_scope/`.

## Core rule

```text
Если artifact связан с initiative, он живет внутри:

operational_scope/initiatives/<initiative-slug>/...

Если artifact не связан с initiative, он живет в соответствующем top-level area:

operational_scope/<artifact-area>/...
```

Иными словами, unscoped path обычно получается из initiative-scoped path удалением segment:

```text
initiatives/<initiative-slug>/
```

Это правило является эвристикой для layout consistency, а не заменяет semantic ownership.

## Raw inputs

Raw / unsorted inputs живут в общем inbox и не переносятся внутрь initiative workspace по умолчанию:

```text
operational_scope/inputs/<artifact-type>/<input-artifact>.md
```

Примеры artifact types:

```text
ideas
plans
feedback
discussions
findings
external
```

Initiative ссылается на inputs через `source-links.md`, который играет роль списка внешних источников / provenance map.

## Initiative workspace

Initiative workspace является namespace для scoped operational artifacts:

```text
operational_scope/initiatives/<initiative-slug>/
  index.md
  source-links.md
  preparation-decisions.md
```

`source-links.md` сохраняет ссылки на external/raw inputs and provenance. Он не заменяет local working artifacts.

## Task artifacts

Task artifacts всегда живут внутри `tasks/` area.

### Initiative-scoped tasks

```text
operational_scope/initiatives/<initiative-slug>/tasks/<task-type>/<task-slug>.md
```

Task types:

```text
execution
research
deep-research
spikes
```

### Unscoped tasks

```text
operational_scope/tasks/<task-type>/<task-slug>.md
```

Examples:

```text
operational_scope/tasks/execution/<task-slug>.md
operational_scope/tasks/research/<task-slug>.md
operational_scope/tasks/deep-research/<task-slug>.md
operational_scope/tasks/spikes/<task-slug>.md
```

## Task maps

Central task map is a navigation index for task scopes:

```text
operational_scope/task-map.md
```

Initiative task map:

```text
operational_scope/initiatives/<initiative-slug>/tasks/task-map.md
```

Unscoped task map:

```text
operational_scope/tasks/task-map.md
```

Task maps can group tasks by sections:

```markdown
## Execution tasks
## Research tasks
## Deep Research tasks
## Spike tasks
```

## Evidence outputs

Evidence output artifacts do not live inside `tasks/`. Tasks describe what must be researched or validated; evidence outputs record what was found.

### Initiative-scoped evidence outputs

```text
operational_scope/initiatives/<initiative-slug>/<evidence-type>/<evidence-slug>/
```

Evidence types:

```text
research
deep-research
spikes
```

Examples:

```text
operational_scope/initiatives/<initiative-slug>/research/<research-slug>/
operational_scope/initiatives/<initiative-slug>/deep-research/<deep-research-slug>/
operational_scope/initiatives/<initiative-slug>/spikes/<spike-slug>/
```

### Unscoped evidence outputs

```text
operational_scope/<evidence-type>/<evidence-slug>/
```

Examples:

```text
operational_scope/research/<research-slug>/
operational_scope/deep-research/<deep-research-slug>/
operational_scope/spikes/<spike-slug>/
```

## Execution outputs

Execution task outputs are project changes themselves:

```text
docs/
services/
contracts/
tests/
assets/
```

Do not create a separate operational output folder for execution task results unless a project-local process explicitly requires it.

## Invariants

- Raw inputs stay in `operational_scope/inputs/<artifact-type>/` and are referenced from initiatives through `source-links.md`.
- Initiative workspace owns scoped working context, scoped tasks and scoped evidence outputs.
- Task artifacts and evidence output artifacts are different artifact types and must not share the same storage path.
- `tasks/<task-type>/` contains task briefs / execution tracking, not evidence reports.
- `<evidence-type>/<evidence-slug>/` contains evidence outputs, not task briefs.
- `operational_scope/task-map.md` is central navigation, while local task maps live in `tasks/task-map.md` or `initiatives/<initiative-slug>/tasks/task-map.md`.
