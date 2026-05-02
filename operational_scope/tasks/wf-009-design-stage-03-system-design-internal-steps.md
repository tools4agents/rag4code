# Task: Design Stage 03 — System Design internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stages и process workflows.

`Stage 03 — System Design` уже имеет stage workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/
  README.md
  workflow.md
```

Текущая задача не должна заново проектировать top-level methodology graph. Нужно проработать внутренний план `workflow-step` для Stage 03, согласовать его с человеком, а затем materialize-ить step packs.

`System Design` работает внутри Early Design Convergence Loop вместе с Discovery and Architecture Design. Его фокус — описать продукт на языке системы: system boundary, external context, system-level behavior, data/state, operational constraints and integration surfaces.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target stage

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
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

Проработать internal steps для `Stage 03 — System Design` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в stage `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность stage workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- System Design internal workflow graph;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- boundaries между System Design, Architecture Design, Discovery and Design Baseline Consolidation;
- system boundary and external context framing;
- system-level behavior and scenario modeling;
- data/state ownership and lifecycle framing;
- operational constraints and NFR handling;
- integration surfaces and external systems;
- места, где возможны Research / Deep Research / Spike Experiments;
- rules for System Design Specification as Specification / SoT Materialization output;
- traceability expectations from system artifacts to product/architecture/contracts/tests/tasks;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- production code;
- project-specific system architecture decisions;
- detailed component design that belongs to Architecture Design;
- test strategy internals that belong to Test Design;
- implementation planning;
- release or cleanup logic.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие system design steps являются обязательными, а какие optional;
- как отличать System Design от Architecture Design;
- нужен ли отдельный step для system boundary and context;
- нужен ли отдельный step для system scenarios and behavior;
- где фиксировать data/state ownership and lifecycle;
- где фиксировать integration surfaces and external systems;
- как handling NFRs and operational constraints влияет на downstream stages;
- какой readiness gate нужен перед выходом в Design Baseline Consolidation;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [x] План internal steps обсужден с человеком до создания step packs.
- [x] Согласованный internal workflow graph добавлен в `stages/03-system-design/workflow.md`.
- [x] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [x] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [x] Каждый step pack имеет `vacancy.md`.
- [x] Step boundaries не дублируют Architecture Design или Test Design.
- [x] System Design Specification описан как output Specification / SoT Materialization, а не отдельная top-level stage.
- [x] Stage workflow не требует hidden knowledge from `operational_scope/` as SoT.
- [x] Links and terminology follow documentation rules.

## Execution Status

- Current State: completed
- Next Step: none
- Blockers: none
- Verification: Stage workflow, step packs and vacancies checked for presence, workflow links and consistency with agreed Stage 03 boundaries.
