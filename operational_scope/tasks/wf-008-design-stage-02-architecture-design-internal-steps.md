# Task: Design Stage 02 — Architecture Design internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stages и process workflows.

`Stage 02 — Architecture Design` уже имеет stage workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/
  README.md
  workflow.md
```

Текущая задача не должна заново проектировать всю методологию или переписывать top-level graph. Нужно проработать внутренний план `workflow-step` для Stage 02, согласовать его с человеком, а затем materialize-ить step packs.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target stage

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)
- [`rules-documentation`](../../assets/rules/rules-documentation)

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Проработать internal steps для `Stage 02 — Architecture Design` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в stage `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность stage workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- Architecture Design internal workflow graph;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- boundaries между Architecture Design, System Design, Test Design and Design Baseline Consolidation;
- правила использования Specification / SoT Materialization для architecture docs, contracts and ADR;
- explicit handling of static architecture and dynamic architecture;
- места, где возможны Research / Deep Research / Spike Experiments;
- traceability expectations from architecture artifacts to product/system/contracts/tests/tasks;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- production code;
- project-specific architecture decisions;
- full implementation planning;
- Test Design internal steps;
- System Design internal steps;
- release or cleanup logic.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие architecture design steps являются обязательными, а какие optional;
- нужен ли отдельный step для static architecture;
- нужен ли отдельный step для dynamic architecture and scenarios;
- где фиксировать contracts and key models внутри Architecture Design;
- как не превращать ADR в обязательный step, но сохранить ADR capture как capability;
- какой readiness gate нужен перед выходом в Design Baseline Consolidation;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `stages/02-architecture-design/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Step boundaries не дублируют System Design или Test Design.
- [ ] ADR описан как capability / SoT materialization option, а не обязательный architecture step.
- [ ] Stage workflow не требует hidden knowledge from `operational_scope/` as SoT.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Architecture Design.
- Blockers: none
- Verification: Проверить stage workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.
