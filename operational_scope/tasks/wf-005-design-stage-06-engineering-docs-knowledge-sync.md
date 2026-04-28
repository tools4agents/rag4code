# Task: Design Stage 06 — Engineering Docs & Knowledge Sync workflow

## Контекст

Нужно разработать Stage 6 как nested workflow. Stage 6 синхронизирует durable engineering docs with implemented and verified state, не смешивая dev SoT с user-facing release docs.

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
- Stage 5 workflow after `wf-004` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/05-integration-verification/workflow.md`

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)

### Documentation and SoT source corpus

- [`software-architecture-documentation-methodology.md`](../../assets/metodologes/waterfall/software-architecture-documentation-methodology.md)
- [`docs-sot-plans-critic-task-flow.md`](../../assets/metodologes/waterfall/new_methodology/docs-sot-plans-critic-task-flow.md)
- [`staged-focus-first-execution.md`](../../assets/metodologes/waterfall/new_methodology/staged-focus-first-execution.md)

### Workflow terms

- [`workflow.md`](../../docs/terms/project/terms/workflow.md)
- [`workflow-step.md`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate.md`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-exchange-layer.md`](../../docs/terms/project/terms/workflow-exchange-layer.md)

## Цель

Создать Stage 6 nested workflow pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/06-engineering-docs-knowledge-sync/
  workflow.md
  steps/*/STEP.md
  resources/
```

## Scope

Включить:

- implemented-state intake;
- docs drift detection;
- engineering SoT update flow;
- ADR/contracts/testing docs sync;
- graph-ready anchor consistency pass;
- docs sync gate;
- release-facing documentation candidates list for Stage 7;
- cleanup recommendations for operational artifacts already promoted to SoT.

Не включать:

- publishing user-facing docs;
- GitHub release creation;
- deleting operational artifacts before sync gate passes.

## Dependencies

- Depends on `wf-004` Stage 5 workflow.
- Should be completed before Stage 7 workflow.

## Definition of Done

- [ ] `stages/06-engineering-docs-knowledge-sync/workflow.md` exists.
- [ ] Stage 6 clearly follows `documentation-lifecycle-layers`.
- [ ] Stage 6 distinguishes engineering SoT from release/user-facing documentation.
- [ ] Stage 6 includes a docs sync gate as `workflow-step-gate`.
- [ ] Stage 6 explains how graph-ready anchors are checked/updated.
- [ ] Stage 6 produces handoff to Stage 7 with release-facing documentation candidates.
- [ ] `software-development-methodology/workflow.md` links to the new Stage 6 workflow.

## Execution Status

- Current State: queued
- Next Step: Design after Stage 5 workflow stabilizes.
- Blockers: `wf-004` should be stabilized first.
- Verification: Ensure Stage 6 does not treat release docs as engineering SoT.
