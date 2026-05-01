# Task: Design Stage 05 — Delivery Planning & Task Decomposition internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stage workflows и process workflows.

`Stage 05 — Delivery Planning & Task Decomposition` уже имеет stage workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/05-delivery-planning-task-decomposition/
  README.md
  workflow.md
```

Этот stage идет после process workflow `Pre-Planning Baseline Freeze`:

```text
Pre-Planning Baseline Freeze
  -> Delivery Planning & Task Decomposition
  -> Task Implementation
```

`Delivery Planning & Task Decomposition` не выполняет SoT freeze и не сокращает большие operational plans. Он consumes self-contained engineering SoT and short implementation plan, подготовленные в `Pre-Planning Baseline Freeze`, и превращает их в executable task set.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target stage

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/05-delivery-planning-task-decomposition/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/05-delivery-planning-task-decomposition/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/pre-planning-baseline-freeze/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/06-task-implementation/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`task-map.template.md`](../../docs/methodology-layer/assets/task-management/resources/task-map.template.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)
- [`rules-documentation`](../../assets/rules/rules-documentation)

### Related skills / assets

Use [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md) for external asset paths.

Relevant assets include:

- Task Management;
- taskset materialization skills, if still used by the workflow-pack;
- task materialization skills, if still used by the workflow-pack;
- Testing System for verification expectation references.

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`workflow-exchange layer`](../../docs/terms/project/terms/workflow-exchange-layer.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Проработать internal steps для `Stage 05 — Delivery Planning & Task Decomposition` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в stage `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность stage workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- Delivery Planning internal workflow graph;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- intake from Pre-Planning Baseline Freeze;
- validation that self-contained SoT and short implementation plan exist;
- taskset planning and decomposition flow;
- delivery slices and task boundaries;
- dependency ordering and current focus rules;
- creation/update rules for `operational_scope/task-map.md`;
- task artifact materialization rules for `operational_scope/tasks/`;
- task-to-SoT link requirements;
- task-level Definition of Done and verification expectations;
- planning readiness / taskset quality gates;
- handoff to Task Implementation;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- SoT freeze or plan cleanup, because it belongs to Pre-Planning Baseline Freeze;
- production code;
- test implementation;
- Integration & Verification internals;
- release or cleanup logic;
- silent product/architecture/system decisions.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие planning steps являются обязательными, а какие optional;
- как проверять, что Pre-Planning Baseline Freeze действительно подготовил valid input;
- как taskset должен ссылаться на short implementation plan and SoT;
- как выбирать task boundaries and delivery slices;
- как фиксировать dependencies and current focus;
- где использовать Task Management asset and task materialization skills;
- какой gate нужен перед materialization tasks;
- какой gate нужен перед handoff to Task Implementation;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/stages/05-delivery-planning-task-decomposition/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `stages/05-delivery-planning-task-decomposition/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Workflow consumes self-contained SoT and short implementation plan from Pre-Planning Baseline Freeze.
- [ ] Workflow не выполняет SoT freeze or plan cleanup.
- [ ] Task files require explicit canonical references, DoD and verification expectations.
- [ ] Return path to Pre-Planning Baseline Freeze exists when input is not ready.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Delivery Planning & Task Decomposition.
- Blockers: none
- Verification: Проверить stage workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.
