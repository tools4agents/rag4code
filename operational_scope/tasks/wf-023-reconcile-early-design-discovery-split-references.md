# Task: Reconcile Early Design Discovery split references

## Контекст

Legacy `Stage 01 — Discovery & Intent Framing` был разделен на три целевых workflow / stage artifacts:

1. [`Initiative Workspace Preparation`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/workflow.md) — process workflow для workspace preparation, source links, provenance and initial route recommendation.
2. [`Opportunity Discovery`](../../assets/metodologes/waterfall/software-development-methodology/workflows/opportunity-discovery/workflow.md) — optional pre-design workflow для opportunity exploration and build/not-build reasoning.
3. [`Product Design`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/workflow.md) — Stage 01 внутри Early Design Convergence Loop, владеющий product intent, value, actors, capabilities, scope, scenarios and acceptance criteria.

Старый путь:

```text
assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md
```

устарел и больше не должен использоваться как current Stage 01 reference в активных methodology tasks.

Pre-split critic finding artifact `operational_scope/findings/critic_early_design_loop_findings.md` был переоценен по текущим workflow artifacts. Его findings закрыты `wf-019`, `wf-020`, `wf-021`, `wf-022` and follow-up traceability tasks, поэтому artifact удален как obsolete temporary finding file.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`human-orchestrated-stage-draft-authoring.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/human-orchestrated-stage-draft-authoring.md)
- [`early-design-stage-boundaries.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/early-design-stage-boundaries.md)

### Removed critic findings

- Obsolete pre-split artifact `operational_scope/findings/critic_early_design_loop_findings.md` was reviewed and removed during this task because no finding remained actionable for the current SDLC workflow state.

### Current split workflow targets

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/opportunity-discovery/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/workflow.md)

### Current SDLC stages and adjacent process workflows

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/05-execution-planning-task-decomposition/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/06-task-implementation/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/07-integration-verification/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/08-engineering-docs-knowledge-sync/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/09-release-cleanup/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/pre-planning-baseline-freeze/workflow.md)

### Task context to reconcile

- [`wf-008-design-stage-02-architecture-design-internal-steps.md`](./wf-008-design-stage-02-architecture-design-internal-steps.md)
- [`wf-009-design-stage-03-system-design-internal-steps.md`](./wf-009-design-stage-03-system-design-internal-steps.md)
- [`wf-010-design-process-design-baseline-consolidation-internal-steps.md`](./wf-010-design-process-design-baseline-consolidation-internal-steps.md)
- [`wf-011-design-stage-04-test-design-internal-steps.md`](./wf-011-design-stage-04-test-design-internal-steps.md)
- [`wf-012-design-process-pre-planning-baseline-freeze-internal-steps.md`](./wf-012-design-process-pre-planning-baseline-freeze-internal-steps.md)
- [`wf-019-design-process-initiative-workspace-preparation.md`](./wf-019-design-process-initiative-workspace-preparation.md) — historical split task; preserve pre-split references as historical context.
- [`wf-020-design-pre-stage-opportunity-discovery.md`](./wf-020-design-pre-stage-opportunity-discovery.md) — historical split task; preserve pre-split references as historical context.
- [`wf-021-redesign-stage-01-product-design-early-design-loop.md`](./wf-021-redesign-stage-01-product-design-early-design-loop.md) — historical split task; preserve pre-split references as historical context.
- [`wf-022-sync-sdlc-workflow-with-pre-design-and-product-design.md`](./wf-022-sync-sdlc-workflow-with-pre-design-and-product-design.md) — historical split synchronization task; preserve pre-split/intermediate naming as historical context.

## Цель

Навести consistency в operational task artifacts после split старого `Discovery & Intent Framing` на `Initiative Workspace Preparation`, `Opportunity Discovery` and `Product Design`.

Нужно:

1. перечитать critic findings и текущие split workflows;
2. проверить, какие findings critic artifact все еще актуальны после `wf-019`–`wf-022`, and remove the obsolete finding artifact if no finding remains actionable;
3. обновить stale references в task artifacts на актуальные paths and names;
4. не переписывать historical split tasks (`wf-019`–`wf-022`), где старое имя используется как historical baseline or intermediate decision history;
5. зафиксировать remaining open consistency issues, если они обнаружены.

## Scope

Включить:

- search по `operational_scope/tasks/*.md` на stale references:
  - `stages/01-discovery-intent-framing/`;
  - `Discovery & Intent Framing` как current stage name;
  - `01-product-design-intent-framing`;
  - `Product Design & Intent Framing` как current canonical stage name, если оно противоречит принятому `Product Design`;
- semantic review of current references: куда должен вести каждый stale reference:
  - `Initiative Workspace Preparation`, если речь о workspace preparation, source links, provenance, initial routing;
  - `Opportunity Discovery`, если речь об exploratory discovery, opportunity, alternatives, build/not-build;
  - `Product Design`, если речь о Stage 01 внутри Early Design Convergence Loop;
- update task reading context links, scope wording, expected outputs and handoff notes where they currently point to stale Stage 01 path/name;
- preserve historical statements in completed tasks when they explain why split happened, but clarify that they refer to legacy state;
- do not edit historical split tasks `wf-019`–`wf-022` only to normalize old names/paths;
- produce a short remaining-findings note inside this task artifact or in handoff notes after execution.

Не включать:

- redesign of Product Design, Opportunity Discovery or Initiative Workspace Preparation;
- removal of legacy `stages/01-discovery-intent-framing/` directory;
- changes to durable methodology SoT unless task review shows a direct broken link in active docs and human agrees;
- creation of new workflow steps;
- `vacancy.md` materialization;
- production code.

## Initial known stale references

Initial grep before creating this task found stale or suspicious references in:

```text
operational_scope/tasks/wf-008-design-stage-02-architecture-design-internal-steps.md
operational_scope/tasks/wf-009-design-stage-03-system-design-internal-steps.md
operational_scope/tasks/wf-010-design-process-design-baseline-consolidation-internal-steps.md
operational_scope/tasks/wf-019-design-process-initiative-workspace-preparation.md
operational_scope/tasks/wf-020-design-pre-stage-opportunity-discovery.md
operational_scope/tasks/wf-021-redesign-stage-01-product-design-early-design-loop.md
operational_scope/tasks/wf-022-sync-sdlc-workflow-with-pre-design-and-product-design.md
```

There may be more. Do not rely only on this list; run a fresh search during execution.

## Critic findings reassessment result

Obsolete pre-split critic input `operational_scope/findings/critic_early_design_loop_findings.md` was reviewed during execution and removed. Findings were classified as:

- `resolved-by-current-workflows`;
- `partially-resolved`;
- `still-actual`;
- `obsolete-after-split`;
- `needs-new-task`.

Verified outcomes:

1. Stage 01 as loop vs pre-loop gate — resolved by `Product Design` and pre-design workflows split.
2. Symmetrical re-entry into Stage 01 — resolved by Product Design re-entry model.
3. Product baseline materialization — resolved by Product Design Step 06 and Design Baseline Consolidation; traceability strengthening is already represented by `wf-024`–`wf-026`.
4. First routing after Stage 01 — resolved by Product Design routing guidance and top-level workflow wording.
5. Stage 02/03 overlap — resolved by local boundary notes.
6. Stage 02/03 direct route to Design Baseline Consolidation — resolved by stage-local contribution wording and Design Baseline Consolidation readiness checks.

## Expected output

После выполнения задачи должны быть обновлены:

```text
operational_scope/tasks/*.md
```

в тех местах, где active task references or reading contexts point to stale current Stage 01 path/name.

Этот task artifact должен быть updated with execution handoff notes summarizing:

- which files were changed;
- which critic findings remain actual;
- which stale references were intentionally preserved as historical context;
- whether a follow-up task is needed.

## Definition of Done

- [x] Fresh search for stale Stage 01 names/paths completed.
- [x] Current split workflow artifacts reviewed.
- [x] Critic findings reassessed against current workflows.
- [x] Obsolete critic finding artifact removed because no finding remains actionable for current SDLC workflow state.
- [x] Active task reading contexts no longer point to `stages/01-discovery-intent-framing/workflow.md` as current Stage 01, excluding historical split tasks intentionally left unchanged.
- [x] References to workspace preparation route to `Initiative Workspace Preparation`.
- [x] References to exploratory opportunity route to `Opportunity Discovery`.
- [x] References to current Stage 01 route to `stages/01-product-design/workflow.md` and `Product Design`.
- [x] Historical legacy references are preserved intentionally in split tasks `wf-019`–`wf-022`.
- [x] No `vacancy.md` expectations are reintroduced contrary to current human-orchestrated draft mode.
- [x] Task handoff notes summarize changed files and remaining issues.

## Execution Status

- Current State: completed
- Completed At: 2026-05-06
- Next Step: none
- Blockers: none
- Verification: fresh grep/search and manual semantic review of updated task links completed.

## Handoff Notes

### Changed files

- Deleted obsolete temporary finding artifact:
  - `operational_scope/findings/critic_early_design_loop_findings.md`
- Updated current task references:
  - [`wf-008-design-stage-02-architecture-design-internal-steps.md`](./wf-008-design-stage-02-architecture-design-internal-steps.md) — adjacent Stage 01 link now points to `stages/01-product-design/workflow.md`.
  - [`wf-009-design-stage-03-system-design-internal-steps.md`](./wf-009-design-stage-03-system-design-internal-steps.md) — current Early Design wording now uses `Product Design`; adjacent Stage 01 link now points to `stages/01-product-design/workflow.md`.
  - [`wf-011-design-stage-04-test-design-internal-steps.md`](./wf-011-design-stage-04-test-design-internal-steps.md) — current return paths now use `Product Design` instead of legacy `Discovery`.
  - This task artifact — updated to record critic finding deletion, split-task preservation policy and execution handoff.

### Critic findings reassessment

The pre-split critic findings no longer contain actionable issues for the current SDLC workflow state:

- Stage 01 as loop vs pre-loop gate — resolved by `Initiative Workspace Preparation`, `Opportunity Discovery` and `Product Design` split.
- Symmetrical re-entry into Stage 01 — resolved by `Product Design` entry/re-entry model.
- Product baseline materialization — resolved by `Product Design` Step 06 and `Design Baseline Consolidation`; traceability strengthening is already captured by `wf-024`–`wf-026`.
- First routing after Stage 01 — resolved by `Product Design` routing guidance and top-level workflow wording.
- Stage 02/03 overlap — resolved by local boundary notes and `early-design-stage-boundaries.md`.
- Stage 02/03 direct route to Design Baseline Consolidation — resolved by stage-local “contribution ready” wording and `Design Baseline Consolidation` cross-stage readiness checks.

Because all findings are resolved, obsolete-after-split or already represented by later tasks, `critic_early_design_loop_findings.md` was removed.

### Historical references intentionally preserved

Per human instruction, tasks dedicated to splitting old Stage 01 were not edited only to normalize historical names/paths:

- `wf-019-design-process-initiative-workspace-preparation.md`
- `wf-020-design-pre-stage-opportunity-discovery.md`
- `wf-021-redesign-stage-01-product-design-early-design-loop.md`
- `wf-022-sync-sdlc-workflow-with-pre-design-and-product-design.md`

Their references to `Discovery & Intent Framing`, `01-discovery-intent-framing`, `Product Design & Intent Framing` or intermediate paths are treated as split history / intermediate decision history, not current Stage 01 guidance.

### Follow-up

No new follow-up task is needed for stale split references. Traceability-related remaining work is already captured by `wf-024`, `wf-025` and `wf-026`.
