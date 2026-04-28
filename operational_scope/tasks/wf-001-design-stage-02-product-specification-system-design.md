# Task: Design Stage 02 — Product Specification & System Design workflow

## Контекст

Нужно разработать Stage 2 как nested workflow внутри `software-development-methodology`.

Stage 2 принимает accepted discovery output из Stage 1 и materialize-ит durable product/system design baseline в engineering SoT: `docs/product/`, `docs/architecture/`, `docs/contracts/`, `docs/adr/`, `docs/testing/`.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Workspace and project context

- [`AGENTS.md`](../../AGENTS.md)
- [`project/index.md`](../../project/index.md)
- [`docs/index.md`](../../docs/index.md)
- [`operational_scope/index.md`](../index.md)

### Workflow methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`baseline-v0.md`](../../assets/metodologes/waterfall/software-development-methodology/decisions/baseline-v0.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/graph-traceability/README.md)

### Stage 1 reference pattern

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- [`discovery-scale-modes.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/resources/discovery-scale-modes.md)
- [`discovery-workspace-lifecycle.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/resources/discovery-workspace-lifecycle.md)
- [`01-intake-context/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/steps/01-intake-context/STEP.md)
- [`02-workspace-activation/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/steps/02-workspace-activation/STEP.md)
- [`06-uncertainty-triage/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/steps/06-uncertainty-triage/STEP.md)
- [`07-evidence-task-setting/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/steps/07-evidence-task-setting/STEP.md)
- [`08-evidence-result-intake/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/steps/08-evidence-result-intake/STEP.md)
- [`09-intent-readiness-gate/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/steps/09-intent-readiness-gate/STEP.md)

### Required dependent assets

- [`project-context-entry-system`](../../docs/methodology-layer/assets/project-context-entry-system/index.md)
- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`test-case-traceability.md`](../../docs/methodology-layer/assets/testing-system/test-case-traceability.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)

### Workflow terms

- [`workflow.md`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack.md`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step.md`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate.md`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack.md`](../../docs/terms/project/terms/workflow-step-pack.md)

### Old source corpus / synthesis inputs

- [`software-architecture-documentation-methodology.md`](../../assets/metodologes/waterfall/software-architecture-documentation-methodology.md)
- [`workflow-map.md`](../../assets/metodologes/waterfall/metodology/workflow-map.md)
- [`02-architect-stage-principles.md`](../../assets/metodologes/waterfall/metodology/stages/02-architect-stage-principles.md)
- [`docs-sot-plans-critic-task-flow.md`](../../assets/metodologes/waterfall/new_methodology/docs-sot-plans-critic-task-flow.md)
- [`critic-findings-freeze-immediately.md`](../../assets/metodologes/waterfall/new_methodology/critic-findings-freeze-immediately.md)

## Цель

Создать Stage 2 nested workflow pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/02-product-specification-system-design/
  workflow.md
  steps/*/STEP.md
  resources/
```

## Scope

Включить:

- Stage 2 workflow graph;
- happy path and return/exception paths;
- step table;
- workflow-step-gates for readiness/freeze decisions;
- resource files/templates when stage-wide concepts become too large for `workflow.md`;
- clear boundary with Stage 1 and Stage 3;
- rules for promoting accepted discovery output into `docs/product/`;
- traceability anchors from product intent to architecture/contracts/ADR/testing.

Не включать:

- implementation tasks;
- production code;
- full graph DB schema;
- project-specific architecture decisions.

## Минимальные expected steps

Список можно уточнить при проектировании, но Stage 2 должен покрыть:

1. Product SoT materialization.
2. Requirement/story/scenario identifier assignment.
3. System design framing.
4. Architecture views and component boundaries.
5. Contract and key model drafting.
6. ADR candidate detection/writing.
7. Testing strategy and traceability planning.
8. Specification/system-design review gate.
9. Stage 3 handoff.

## Dependencies

- Depends on completed Stage 1 workflow baseline.
- Should be completed before tasks `wf-002` through `wf-006` are finalized.

## Definition of Done

- [ ] `stages/02-product-specification-system-design/workflow.md` exists.
- [ ] Stage 2 is modeled as nested workflow, not one large `STEP.md`.
- [ ] Each meaningful semantic routing decision is materialized as `workflow-step-gate`.
- [ ] Each workflow-step has bounded inputs/actions/outputs/DoD/return conditions.
- [ ] Stage 2 explains how accepted discovery output becomes durable `docs/product/` and system design SoT.
- [ ] Stage 2 establishes graph-ready anchor expectations for product, architecture, contracts, ADR and testing artifacts.
- [ ] `software-development-methodology/workflow.md` links to the new Stage 2 workflow.
- [ ] No legacy `tasks_descriptions/` terminology is introduced.

## Execution Status

- Current State: queued
- Next Step: Design Stage 2 workflow skeleton using Stage 1 as structural pattern.
- Blockers: none
- Verification: Review generated files for progressive disclosure, link correctness and conformance to workflow terms.
