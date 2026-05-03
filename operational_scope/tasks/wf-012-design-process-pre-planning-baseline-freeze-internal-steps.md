# Task: Design process workflow — Pre-Planning Baseline Freeze internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stage workflows и process workflows.

`Pre-Planning Baseline Freeze` уже имеет process workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/workflows/pre-planning-baseline-freeze/
  README.md
  workflow.md
```

Этот workflow расположен между `Stage 04 — Test Design` и `Stage 05 — Execution Planning & Task Decomposition`:

```text
Test Design
  -> Pre-Planning Baseline Freeze
  -> Execution Planning & Task Decomposition
```

Его задача — после Test Design зафиксировать self-contained engineering SoT для selected scope, учесть findings из Test Design и подготовить short implementation plan, из которого можно создавать tasks.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target process workflow

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/pre-planning-baseline-freeze/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/pre-planning-baseline-freeze/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/05-execution-planning-task-decomposition/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`test-case-traceability.md`](../../docs/methodology-layer/assets/testing-system/test-case-traceability.md)
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

Проработать internal steps для process workflow `Pre-Planning Baseline Freeze` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в process `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность process workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- internal workflow graph для Pre-Planning Baseline Freeze;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- intake of Test Design outputs and findings;
- final SoT completeness and consistency review for selected implementation scope;
- проверку, что operational_scope больше не является hidden SoT;
- plan cleanup / shortening до short implementation plan with links to SoT;
- handling of blockers, white spots and open questions;
- routing to Early Design Convergence Loop, Test Design, Research / Deep Research / Spike Experiments;
- readiness decision for Execution Planning & Task Decomposition;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- task-map creation;
- implementation task materialization;
- production code;
- test implementation;
- release or cleanup logic;
- rewriting all SoT from scratch if only focused updates are needed.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие checks обязательны перед Execution Planning;
- что значит self-contained SoT for selected implementation scope;
- как учитывать findings из Test Design;
- как определить, что operational plan слишком длинный и дублирует SoT;
- каким должен быть short implementation plan;
- нужен ли отдельный step для plan cleanup / shortening;
- нужен ли отдельный critic/review step для SoT completeness and non-contradiction;
- какие verdicts должен иметь planning readiness gate;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/workflows/pre-planning-baseline-freeze/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `workflows/pre-planning-baseline-freeze/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Workflow проверяет SoT completeness, consistency and non-contradiction для selected implementation scope.
- [ ] Workflow создает или требует short implementation plan with links to SoT.
- [ ] Workflow явно не создает task-map и implementation tasks.
- [ ] Workflow может вернуть gaps в Test Design, Early Design Convergence Loop или Research/Spike.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Pre-Planning Baseline Freeze.
- Blockers: none
- Verification: Проверить process workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.
