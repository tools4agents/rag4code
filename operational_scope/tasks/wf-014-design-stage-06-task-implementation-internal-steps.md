# Task: Design Stage 06 — Task Implementation internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stage workflows и process workflows.

`Stage 06 — Task Implementation` уже имеет stage workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/06-task-implementation/
  README.md
  workflow.md
```

Этот stage идет после `Stage 05 — Delivery Planning & Task Decomposition` и перед `Stage 07 — Integration & Verification`:

```text
Delivery Planning & Task Decomposition
  -> Task Implementation
  -> Integration & Verification
```

`Task Implementation` реализует bounded tasks, подготовленные на planning stage. Он не должен silently принимать product / architecture / system decisions, если во время реализации обнаруживается gap. Такие gaps должны быть явно routed назад в appropriate workflow.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target stage

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/06-task-implementation/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/06-task-implementation/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/05-delivery-planning-task-decomposition/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/07-integration-verification/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/pre-planning-baseline-freeze/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`test-case-traceability.md`](../../docs/methodology-layer/assets/testing-system/test-case-traceability.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)
- [`rules-documentation`](../../assets/rules/rules-documentation)

### Related assets

Use [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md) for external asset paths.

Relevant assets include:

- Task Management;
- Testing System;
- Documentation Rules;
- Research / Spike if implementation reveals uncertainty that requires evidence.

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`workflow-exchange layer`](../../docs/terms/project/terms/workflow-exchange-layer.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Проработать internal steps для `Stage 06 — Task Implementation` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в stage `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность stage workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- Task Implementation internal workflow graph;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- task intake and task readiness validation;
- reading task artifact, task-map context, short implementation plan context and linked SoT;
- bounded implementation planning inside one task;
- code change execution boundary;
- test implementation/update boundary;
- local verification and task-level checks;
- design-gap detection and return paths;
- task status update and handoff evidence;
- code/test traceability expectations;
- handoff to Integration & Verification;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- broad integration verification across multiple tasks;
- release cleanup;
- large redesign inside implementation;
- silent architecture/product/system decisions;
- creating new task sets unless returning to Delivery Planning;
- publishing release-facing docs.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие implementation steps являются обязательными, а какие optional;
- как проверять task readiness перед началом implementation;
- где проходит boundary между local task verification and Integration & Verification;
- как фиксировать design gaps, обнаруженные во время implementation;
- когда implementation может update tests внутри task, а когда нужно вернуть в Test Design;
- как обновлять task status and handoff evidence;
- какие code/test traceability anchors нужны;
- какой gate нужен перед handoff to Integration & Verification;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/stages/06-task-implementation/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `stages/06-task-implementation/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Workflow требует task readiness validation before implementation.
- [ ] Workflow сохраняет explicit return paths for design gaps.
- [ ] Workflow не позволяет silent product/architecture/system decisions during implementation.
- [ ] Workflow требует task status update and handoff evidence.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Task Implementation.
- Blockers: none
- Verification: Проверить stage workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.
