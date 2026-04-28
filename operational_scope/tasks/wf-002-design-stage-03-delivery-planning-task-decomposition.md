# Task: Design Stage 03 — Delivery Planning & Task Decomposition workflow

## Контекст

Нужно разработать Stage 3 как nested workflow. Stage 3 превращает engineering SoT, созданный на Stage 2, в executable task set через `operational_scope/task-map.md` и `operational_scope/tasks/`.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Workspace and methodology baseline

- [`AGENTS.md`](../../AGENTS.md)
- [`project/index.md`](../../project/index.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`baseline-v0.md`](../../assets/metodologes/waterfall/software-development-methodology/decisions/baseline-v0.md)

### Stage workflows to use as upstream/reference

- [`01-discovery-intent-framing/workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- Stage 2 workflow after `wf-001` is completed: `assets/metodologes/waterfall/software-development-methodology/stages/02-product-specification-system-design/workflow.md`

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`task-map.template.md`](../../docs/methodology-layer/assets/task-management/resources/task-map.template.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)

### Task materialization skills and rules

- [`taskset-materializer/SKILL.md`](../../assets/skills/task-managment/taskset-materializer/SKILL.md)
- [`task-materializer/SKILL.md`](../../assets/skills/task-managment/task-materializer/SKILL.md)
- [`task-map-approach.md`](../../assets/metodologes/waterfall/new_methodology/task-map-approach.md)
- [`staged-focus-first-execution.md`](../../assets/metodologes/waterfall/new_methodology/staged-focus-first-execution.md)
- [`docs-sot-plans-critic-task-flow.md`](../../assets/metodologes/waterfall/new_methodology/docs-sot-plans-critic-task-flow.md)
- [`stage-3-manual-orchestration.md`](../../assets/metodologes/waterfall/metodology/stage-3-manual-orchestration.md)

### Workflow terms

- [`workflow.md`](../../docs/terms/project/terms/workflow.md)
- [`workflow-step.md`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate.md`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-exchange-layer.md`](../../docs/terms/project/terms/workflow-exchange-layer.md)
- [`step-vacancy.md`](../../docs/terms/project/terms/step-vacancy.md)
- [`prompt-steering.md`](../../docs/terms/project/terms/resources/step-vacancy/prompt-steering.md)

## Цель

Создать Stage 3 nested workflow pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/03-delivery-planning-task-decomposition/
  workflow.md
  steps/*/STEP.md
  resources/
```

## Scope

Включить:

- workflow graph from SoT readiness to taskset materialization;
- taskset planning and decomposition flow;
- planning readiness gate;
- task-map/task artifact materialization boundary;
- rules that tasks must reference `docs/`, contracts, ADR and testing docs rather than temporary plans;
- small-batch/focus-first execution rules;
- dependency ordering and current focus rules;
- Stage 4 handoff.

Не включать:

- implementation execution;
- code changes;
- changing Stage 2 SoT except via explicit return path.

## Dependencies

- Depends on `wf-001` Stage 2 workflow design.
- Must preserve task-management asset contracts.

## Definition of Done

- [ ] `stages/03-delivery-planning-task-decomposition/workflow.md` exists.
- [ ] Stage 3 describes how engineering SoT becomes task-map and task files.
- [ ] Stage 3 uses `workflow-step-gate` for planning readiness and taskset quality decisions.
- [ ] Each workflow-step folder contains `vacancy.md` with role-selection and prompt-steering requirements.
- [ ] Task materialization boundaries point to `taskset-materializer` and `task-materializer` skills.
- [ ] Task files are required to include explicit canonical references and DoD.
- [ ] Return path to Stage 2 exists when SoT is incomplete.
- [ ] `software-development-methodology/workflow.md` links to the new Stage 3 workflow.

## Execution Status

- Current State: queued
- Next Step: Wait for Stage 2 workflow skeleton or use `wf-001` output as upstream reference.
- Blockers: `wf-001` should be stabilized first.
- Verification: Check that Stage 3 does not allow tasks to be created from temporary plans as primary SoT.
