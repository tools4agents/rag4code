# Task: Design Stage 05 — Integration & Verification workflow

## Контекст

Нужно разработать Stage 5 как nested workflow. Stage 5 проверяет, что outputs отдельных task implementations работают вместе как система и что traceability между requirements, tasks, code and tests не разрушена.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`AGENTS.md`](../../AGENTS.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`baseline-v0.md`](../../assets/metodologes/waterfall/software-development-methodology/decisions/baseline-v0.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/graph-traceability/README.md)

### Upstream stage workflows

- Stage 2 workflow after `wf-001` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/02-product-specification-system-design/workflow.md`
- Stage 3 workflow after `wf-002` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/03-delivery-planning-task-decomposition/workflow.md`
- Stage 4 workflow after `wf-003` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/04-task-implementation/workflow.md`

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`test-case-traceability.md`](../../docs/methodology-layer/assets/testing-system/test-case-traceability.md)
- [`test-suites.md`](../../docs/methodology-layer/assets/testing-system/test-suites.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)

### Workflow terms

- [`workflow.md`](../../docs/terms/project/terms/workflow.md)
- [`workflow-step.md`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate.md`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-exchange-layer.md`](../../docs/terms/project/terms/workflow-exchange-layer.md)
- [`step-vacancy.md`](../../docs/terms/project/terms/step-vacancy.md)
- [`prompt-steering.md`](../../docs/terms/project/terms/resources/step-vacancy/prompt-steering.md)

## Цель

Создать Stage 5 nested workflow pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/05-integration-verification/
  workflow.md
  steps/*/STEP.md
  resources/
```

## Scope

Включить:

- integration readiness intake;
- aggregation of completed task outputs;
- contract/system/e2e verification flow;
- defect task creation/return path;
- verification evidence recording;
- integration verification gate;
- traceability consistency check;
- Stage 6 handoff.

Не включать:

- release publication;
- user-facing documentation publication;
- broad docs rewrite except verification-driven corrections.

## Dependencies

- Depends on `wf-003` Stage 4 workflow.
- Should be completed before Stage 6 workflow.

## Definition of Done

- [ ] `stages/05-integration-verification/workflow.md` exists.
- [ ] Stage 5 models integration and verification as a nested workflow.
- [ ] Stage 5 includes verification gate as `workflow-step-gate`.
- [ ] Each workflow-step folder contains `vacancy.md` with role-selection and prompt-steering requirements.
- [ ] Stage 5 defines how failures become defect tasks or return paths.
- [ ] Stage 5 records verification evidence and traceability check expectations.
- [ ] `software-development-methodology/workflow.md` links to the new Stage 5 workflow.

## Execution Status

- Current State: queued
- Next Step: Design after Stage 4 workflow stabilizes.
- Blockers: `wf-003` should be stabilized first.
- Verification: Ensure Stage 5 clearly separates integration verification from docs sync and release cleanup.
