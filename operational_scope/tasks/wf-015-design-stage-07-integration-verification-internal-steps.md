# Task: Design Stage 07 — Integration & Verification internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stage workflows и process workflows.

`Stage 07 — Integration & Verification` уже имеет stage workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/07-integration-verification/
  README.md
  workflow.md
```

Этот stage идет после `Stage 06 — Task Implementation` и перед `Stage 08 — Engineering Docs & Knowledge Sync`:

```text
Task Implementation
  -> Integration & Verification
  -> Engineering Docs & Knowledge Sync
```

`Integration & Verification` проверяет, что outputs реализованных tasks работают вместе как система, а не только локально внутри отдельных tasks. Verification failure является evidence и должен приводить к explicit return path, defect task или recorded rationale.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target stage

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/07-integration-verification/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/07-integration-verification/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/06-task-implementation/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/08-engineering-docs-knowledge-sync/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/05-execution-planning-task-decomposition/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`test-suites.md`](../../docs/methodology-layer/assets/testing-system/test-suites.md)
- [`test-case-traceability.md`](../../docs/methodology-layer/assets/testing-system/test-case-traceability.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)
- [`rules-documentation`](../../assets/rules/rules-documentation)

### Related assets

Use [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md) for external asset paths.

Relevant assets include:

- Testing System;
- Task Management;
- Documentation Rules;
- Research / Spike if verification reveals uncertainty that requires evidence.

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`workflow-exchange layer`](../../docs/terms/project/terms/workflow-exchange-layer.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Проработать internal steps для `Stage 07 — Integration & Verification` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в stage `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность stage workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- Integration & Verification internal workflow graph;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- integration readiness intake;
- aggregation of implemented task outputs;
- selection or execution of relevant checks based on Test Design baseline;
- unit / integration / contract / e2e / smoke / regression checks where relevant;
- verification evidence recording;
- defect and regression classification;
- defect task recommendation or return path;
- traceability check between requirements, tasks, code and tests;
- integration verification gate;
- handoff to Engineering Docs & Knowledge Sync;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- implementation of fixes without task/context boundary;
- broad docs sync beyond verification-driven corrections;
- release-facing documentation publication;
- silent product/architecture/system decisions;
- Test Design strategy redesign except through return path.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие verification steps являются обязательными, а какие optional;
- как выбирать relevant checks based on selected scope and risk profile;
- как отличать local task verification от Integration & Verification;
- как фиксировать verification evidence;
- как классифицировать failed/flaky checks;
- когда failure должен стать defect task, а когда return path;
- как проверять traceability между requirements, tasks, code and tests;
- какой gate нужен перед Engineering Docs & Knowledge Sync;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/stages/07-integration-verification/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `stages/07-integration-verification/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Workflow clearly separates local task verification from integration/system verification.
- [ ] Workflow records verification evidence and traceability check expectations.
- [ ] Workflow defines how failures become defect tasks, return paths or recorded rationale.
- [ ] Workflow has explicit handoff to Engineering Docs & Knowledge Sync.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Integration & Verification.
- Blockers: none
- Verification: Проверить stage workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.
