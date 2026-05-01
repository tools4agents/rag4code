# Task: Design Stage 08 — Engineering Docs & Knowledge Sync internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stage workflows и process workflows.

`Stage 08 — Engineering Docs & Knowledge Sync` уже имеет stage workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/08-engineering-docs-knowledge-sync/
  README.md
  workflow.md
```

Этот stage идет после `Stage 07 — Integration & Verification` и перед `Stage 09 — Release & Cleanup`:

```text
Integration & Verification
  -> Engineering Docs & Knowledge Sync
  -> Release & Cleanup
```

`Engineering Docs & Knowledge Sync` синхронизирует durable engineering documentation с реализованным и verified state. Он нужен, чтобы `docs/` оставались engineering SoT, а принятое знание не оставалось только в code, tasks, verification evidence or operational notes.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target stage

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/08-engineering-docs-knowledge-sync/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/08-engineering-docs-knowledge-sync/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/07-integration-verification/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/09-release-cleanup/workflow.md)
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

- Documentation Rules;
- Testing System;
- Task Management;
- Architect ADR Writer, if implementation/verification surfaced durable decisions that require ADR.

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`workflow-exchange layer`](../../docs/terms/project/terms/workflow-exchange-layer.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Проработать internal steps для `Stage 08 — Engineering Docs & Knowledge Sync` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в stage `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность stage workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- Engineering Docs & Knowledge Sync internal workflow graph;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- intake of implementation outputs and verification evidence;
- docs drift detection;
- affected docs identification;
- engineering SoT update flow;
- architecture / system design / contracts / ADR / testing docs sync;
- traceability anchors and links update;
- check that operational artifacts no longer contain hidden durable decisions;
- release-facing documentation candidates list for Release & Cleanup;
- docs sync readiness gate;
- handoff to Release & Cleanup;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- release docs publication;
- user-facing documentation update execution if it belongs to Release & Cleanup;
- production code changes;
- integration verification execution;
- operational cleanup before durable knowledge is synced;
- new product/architecture decisions without explicit routing and rationale.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие docs sync steps являются обязательными, а какие optional;
- как выявлять docs affected by implemented and verified changes;
- как проверять docs/code/tests consistency;
- как обновлять architecture, contracts, ADR and testing docs;
- как отличать engineering SoT от release docs;
- как фиксировать release-facing documentation candidates for Stage 09;
- какой gate нужен перед Release & Cleanup;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/stages/08-engineering-docs-knowledge-sync/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `stages/08-engineering-docs-knowledge-sync/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Workflow follows documentation-lifecycle-layers.
- [ ] Workflow distinguishes engineering SoT from release docs.
- [ ] Workflow explains how graph-ready anchors are checked/updated.
- [ ] Workflow produces handoff to Release & Cleanup with release-facing documentation candidates.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Engineering Docs & Knowledge Sync.
- Blockers: none
- Verification: Проверить stage workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.
