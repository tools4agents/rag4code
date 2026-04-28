# Task: Design Stage 04 — Task Implementation workflow

## Контекст

Нужно разработать Stage 4 как nested workflow. Stage 4 исполняет bounded task artifacts, производит code/test changes и сохраняет traceability anchors without silent design decisions.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`AGENTS.md`](../../AGENTS.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`baseline-v0.md`](../../assets/metodologes/waterfall/software-development-methodology/decisions/baseline-v0.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/graph-traceability/README.md)

### Upstream stage workflows

- [`01-discovery-intent-framing/workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- Stage 2 workflow after `wf-001` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/02-product-specification-system-design/workflow.md`
- Stage 3 workflow after `wf-002` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/03-delivery-planning-task-decomposition/workflow.md`

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

### Source corpus / implementation principles

- [`docs-sot-plans-critic-task-flow.md`](../../assets/metodologes/waterfall/new_methodology/docs-sot-plans-critic-task-flow.md)
- [`staged-focus-first-execution.md`](../../assets/metodologes/waterfall/new_methodology/staged-focus-first-execution.md)

## Цель

Создать Stage 4 nested workflow pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/04-task-implementation/
  workflow.md
  steps/*/STEP.md
  resources/
```

## Scope

Включить:

- task intake/readiness step;
- implementation planning inside one bounded task;
- code change execution boundary;
- test implementation/update boundary;
- local verification;
- design-gap detection and return path to Stage 2 or Stage 3;
- task status/handoff update;
- code/test traceability anchor expectations.

Не включать:

- broad integration verification across multiple tasks;
- release cleanup;
- creating new architecture decisions silently during implementation.

## Dependencies

- Depends on `wf-002` Stage 3 workflow.
- Should be designed before Stage 5 workflow.

## Definition of Done

- [ ] `stages/04-task-implementation/workflow.md` exists.
- [ ] Stage 4 shows how a bounded task is implemented with code and tests.
- [ ] Stage 4 has explicit return path if implementation reveals SoT/design gap.
- [ ] Stage 4 requires updating task execution status and handoff evidence.
- [ ] Stage 4 preserves traceability from task to code and tests.
- [ ] `software-development-methodology/workflow.md` links to the new Stage 4 workflow.

## Execution Status

- Current State: queued
- Next Step: Design after Stage 3 task decomposition workflow stabilizes.
- Blockers: `wf-002` should be stabilized first.
- Verification: Ensure Stage 4 cannot bypass missing docs/contracts/ADR by silent implementation decisions.
