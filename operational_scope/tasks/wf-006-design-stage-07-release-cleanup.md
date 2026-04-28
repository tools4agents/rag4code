# Task: Design Stage 07 — Release & Cleanup workflow

## Контекст

Нужно разработать Stage 7 как nested workflow. Stage 7 закрывает итерацию: готовит release-facing outputs для project-specific publishing system, фиксирует changelog/release notes inputs и очищает temporary operational context.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`AGENTS.md`](../../AGENTS.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`baseline-v0.md`](../../assets/metodologes/waterfall/software-development-methodology/decisions/baseline-v0.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/graph-traceability/README.md)

### Upstream stage workflows

- Stage 5 workflow after `wf-004` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/05-integration-verification/workflow.md`
- Stage 6 workflow after `wf-005` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/06-engineering-docs-knowledge-sync/workflow.md`

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)

### Release workflow reference

- [`realise_project/workflow.md`](../../assets/workflows/realise_project/workflow.md)
- [`realise_project/01-readiness-gate/STEP.md`](../../assets/workflows/realise_project/01-readiness-gate/STEP.md)
- [`realise_project/terms.md`](../../assets/workflows/realise_project/terms.md)

### Source corpus / cleanup principles

- [`docs-sot-plans-critic-task-flow.md`](../../assets/metodologes/waterfall/new_methodology/docs-sot-plans-critic-task-flow.md)
- [`task-map-approach.md`](../../assets/metodologes/waterfall/new_methodology/task-map-approach.md)
- [`staged-focus-first-execution.md`](../../assets/metodologes/waterfall/new_methodology/staged-focus-first-execution.md)

### Workflow terms

- [`workflow.md`](../../docs/terms/project/terms/workflow.md)
- [`workflow-step.md`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate.md`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-exchange-layer.md`](../../docs/terms/project/terms/workflow-exchange-layer.md)

## Цель

Создать Stage 7 nested workflow pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/07-release-cleanup/
  workflow.md
  steps/*/STEP.md
  resources/
```

## Scope

Включить:

- release readiness intake after Stage 6;
- release-facing documentation update preparation for project-specific publishing system;
- changelog/GitHub release input preparation when applicable;
- operational artifact cleanup policy;
- task-map closure/archive rules;
- graph sync/snapshot checkpoint recommendation;
- release cleanup gate;
- distinction from `realise_project` concrete release publication workflow.

Не включать:

- hardcoded Docusaurus assumptions;
- hardcoded GitHub release policy;
- project-specific release branch/version policy;
- deleting operational artifacts that still contain unpromoted durable knowledge.

## Dependencies

- Depends on `wf-005` Stage 6 workflow.
- Should reference but not duplicate concrete `realise_project` workflow semantics.

## Definition of Done

- [ ] `stages/07-release-cleanup/workflow.md` exists.
- [ ] Stage 7 clearly distinguishes generic SDLC release/cleanup from project-specific release workflow.
- [ ] Stage 7 explains user-facing documentation update preparation without hardcoding Docusaurus.
- [ ] Stage 7 includes cleanup/readiness gate as `workflow-step-gate`.
- [ ] Stage 7 defines when operational artifacts may be archived or removed.
- [ ] Stage 7 includes graph sync/snapshot checkpoint guidance as derived representation, not SoT.
- [ ] `software-development-methodology/workflow.md` links to the new Stage 7 workflow.

## Execution Status

- Current State: queued
- Next Step: Design after Stage 6 workflow stabilizes.
- Blockers: `wf-005` should be stabilized first.
- Verification: Ensure Stage 7 does not turn temporary release preparation history into durable engineering SoT unless project policy explicitly requires it.
