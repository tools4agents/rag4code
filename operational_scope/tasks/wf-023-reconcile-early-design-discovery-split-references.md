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

Есть critic finding artifact [`critic_early_design_loop_findings.md`](../findings/critic_early_design_loop_findings.md), написанный до split. Его findings нужно переоценить по текущим workflow artifacts: часть уже закрыта `wf-019`, `wf-020`, `wf-021` and `wf-022`, часть может остаться актуальной как follow-up.

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

### Critic findings

- [`critic_early_design_loop_findings.md`](../findings/critic_early_design_loop_findings.md)

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
- [`wf-019-design-process-initiative-workspace-preparation.md`](./wf-019-design-process-initiative-workspace-preparation.md)
- [`wf-020-design-pre-stage-opportunity-discovery.md`](./wf-020-design-pre-stage-opportunity-discovery.md)
- [`wf-021-redesign-stage-01-product-design-early-design-loop.md`](./wf-021-redesign-stage-01-product-design-early-design-loop.md)
- [`wf-022-sync-sdlc-workflow-with-pre-design-and-product-design.md`](./wf-022-sync-sdlc-workflow-with-pre-design-and-product-design.md)

## Цель

Навести consistency в operational task artifacts после split старого `Discovery & Intent Framing` на `Initiative Workspace Preparation`, `Opportunity Discovery` and `Product Design`.

Нужно:

1. перечитать critic findings и текущие split workflows;
2. проверить, какие findings critic artifact все еще актуальны после `wf-019`–`wf-022`;
3. обновить stale references в task artifacts на актуальные paths and names;
4. не переписывать historical context там, где старое имя используется как historical baseline, но явно отделить historical references от current references;
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

## Critic findings reassessment guidance

Use [`critic_early_design_loop_findings.md`](../findings/critic_early_design_loop_findings.md) as historical critic input, then classify each finding as one of:

- `resolved-by-current-workflows`;
- `partially-resolved`;
- `still-actual`;
- `obsolete-after-split`;
- `needs-new-task`.

Expected likely outcomes to verify, not assume:

1. Stage 01 as loop vs pre-loop gate — likely resolved by `Product Design` and pre-design workflows split.
2. Symmetrical re-entry into Stage 01 — likely resolved by Product Design re-entry model.
3. Product baseline materialization — likely resolved or partially resolved by Product Design Step 06 and Design Baseline Consolidation.
4. First routing after Stage 01 — likely resolved by Product Design routing guidance and top-level workflow wording.
5. Stage 02/03 overlap — likely resolved or partially resolved by local boundary notes.
6. Stage 02/03 direct route to Design Baseline Consolidation — likely still needs careful wording check in stage-local tasks and workflow docs.

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

- [ ] Fresh search for stale Stage 01 names/paths completed.
- [ ] Current split workflow artifacts reviewed.
- [ ] Critic findings reassessed against current workflows.
- [ ] Active task reading contexts no longer point to `stages/01-discovery-intent-framing/workflow.md` as current Stage 01.
- [ ] References to workspace preparation route to `Initiative Workspace Preparation`.
- [ ] References to exploratory opportunity route to `Opportunity Discovery`.
- [ ] References to current Stage 01 route to `stages/01-product-design/workflow.md` and `Product Design`.
- [ ] Historical legacy references are either preserved intentionally or clarified as historical.
- [ ] No `vacancy.md` expectations are reintroduced contrary to current human-orchestrated draft mode.
- [ ] Task handoff notes summarize changed files and remaining issues.

## Execution Status

- Current State: queued
- Next Step: Run fresh grep/search, reassess critic findings against current workflow docs, then update affected task artifacts.
- Blockers: none
- Verification: grep for stale references and manual semantic review of updated task links.
