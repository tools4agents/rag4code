# Task: Synchronize SDLC workflow graph with pre-design workflows and Product Design

## Контекст

После разделения responsibilities нужно синхронизировать top-level `software-development-methodology/workflow.md` и related methodology references.

Целевая модель:

```text
Preflight
  -> project context loading

Pre-design / process workflows
  -> Initiative Workspace Preparation
  -> Opportunity Discovery
  -> Research / Deep Research / Spike Experiments

Early Design Convergence Loop
  -> 01 Product Design & Intent Framing
  <-> 02 Architecture Design
  <-> 03 System Design
```

Top-level workflow должен перестать позиционировать Stage 01 как both pre-loop and in-loop `Discovery` stage.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)

### Updated/new workflow targets

- `assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/workflow.md`
- `assets/metodologes/waterfall/software-development-methodology/workflows/opportunity-discovery/workflow.md`
- `assets/metodologes/waterfall/software-development-methodology/stages/01-product-design-intent-framing/workflow.md`
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

### Findings and resources

- [`critic_early_design_loop_findings.md`](../findings/critic_early_design_loop_findings.md)
- [`early-design-stage-boundaries.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/early-design-stage-boundaries.md)

## Цель

Синхронизировать top-level SDLC workflow graph and vertex map после выделения `Initiative Workspace Preparation`, `Opportunity Discovery` and `Product Design & Intent Framing`.

## Scope

Включить:

- update top-level process graph;
- update workflow vertex map;
- clarify stage vs process workflow vs pre-stage workflow terminology;
- route rules between pre-design workflows and Early Design Convergence Loop;
- update Early Design Convergence Loop boundary wording;
- ensure Stage 01 naming/path links are consistent;
- ensure Design Baseline Consolidation still remains the only transition to Test Design;
- update cross-cutting workflow notes if needed;
- record unresolved migration issues if any.

Не включать:

- redesign internal steps of Stage 02 or Stage 03 unless links/names must be synchronized;
- implementation tasks;
- production code;
- full Test Design redesign.

## Suggested discussion topics

Перед обновлением top-level workflow обсудить с человеком:

- должен ли Opportunity Discovery быть shown in main process graph или described as optional pre-design workflow;
- должен ли Initiative Workspace Preparation быть shown as process vertex or preflight-like preparation;
- canonical naming for Stage 01 and path migration;
- first routing policy after Product Design: System Design first, Architecture Design first or dynamic route;
- how to represent bidirectional Product/System/Architecture convergence without implying all stages must always be fully executed.

## Expected output

После выполнения задачи должны быть обновлены:

```text
assets/metodologes/waterfall/software-development-methodology/workflow.md
assets/metodologes/waterfall/software-development-methodology/resources/early-design-stage-boundaries.md
```

При необходимости:

```text
assets/metodologes/waterfall/software-development-methodology/README.md
assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md
assets/metodologes/waterfall/software-development-methodology/roles.md
```

## Definition of Done

- [ ] Top-level graph distinguishes pre-design workflows from Early Design Convergence Loop stages.
- [ ] Stage 01 is named and described as Product Design / Intent Framing inside Early Design Convergence Loop.
- [ ] `Initiative Workspace Preparation` and `Opportunity Discovery` links are present and semantically correct.
- [ ] Vertex map does not describe Stage 01 as pre-loop handoff workflow.
- [ ] Boundary resource terminology is synchronized with Product Design naming.
- [ ] Design Baseline Consolidation remains the only allowed transition from Early Design Convergence Loop to Test Design.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: run after target workflow artifacts exist or after their naming/path decisions are frozen.
- Blockers: depends on `wf-019`, `wf-020`, and `wf-021` decisions.
- Verification: pending
