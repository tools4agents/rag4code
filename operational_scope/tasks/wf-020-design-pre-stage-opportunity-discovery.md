# Task: Design pre-stage workflow — Opportunity Discovery

## Контекст

В текущем `Stage 01 — Discovery & Intent Framing` слово `Discovery` смешивает Product Design внутри Early Design Convergence Loop с pre-design exploratory work.

Нужно выделить отдельный pre-stage workflow `Opportunity Discovery`, который исследует problem/opportunity space до появления bounded product initiative.

Этот workflow не является частью Early Design Convergence Loop. Его output — candidate initiative, opportunity hypothesis, backlog candidate, research finding или decision not to proceed.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)

### Current Stage 01 and findings

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- [`critic_early_design_loop_findings.md`](../findings/critic_early_design_loop_findings.md)

### Related context

- [`early-design-stage-boundaries.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/early-design-stage-boundaries.md)
- [`discovery-scale-modes.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/resources/discovery-scale-modes.md)
- [`source-links.template.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/resources/source-links.template.md)

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Спроектировать и materialize-ить pre-stage workflow `Opportunity Discovery`.

Workflow должен отвечать за:

1. exploratory idea/problem intake;
2. problem space and opportunity framing;
3. pain/interview/research finding intake;
4. existing solutions / alternatives scan;
5. candidate opportunity synthesis;
6. opportunity uncertainty and evidence needs;
7. decision whether to create bounded initiative for Product Design.

## Scope

Включить:

- pre-stage workflow graph;
- steps and gates для opportunity exploration;
- research/deep research routing;
- outputs: candidate initiative, opportunity hypothesis, rejected/deferred idea, research finding;
- boundary with `Initiative Workspace Preparation`;
- boundary with `Product Design & Intent Framing`;
- rule that Opportunity Discovery does not produce final product/system/architecture SoT;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- final product scope decisions;
- system boundary design;
- architecture design;
- implementation task decomposition;
- Test Design;
- production code.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие виды discovery поддерживаются: brainstorm, market/existing solution research, interview/pain analysis, problem exploration;
- когда Opportunity Discovery можно пропустить;
- как Opportunity Discovery создает candidate initiative для Product Design;
- где хранить opportunity artifacts: `operational_scope/discovery/`, `operational_scope/opportunities/` или общий initiative workspace;
- какие evidence outputs должны быть linked downstream;
- какие gate verdicts нужны: proceed-to-product-design, need-research, split-opportunity, defer, reject.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/workflows/opportunity-discovery/
  README.md
  workflow.md
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

Возможно обновление Stage 01 naming/resources, если текущие discovery assets будут split or migrated.

## Definition of Done

- [x] План workflow steps обсужден с человеком до создания step packs.
- [x] `Opportunity Discovery` оформлен как pre-stage workflow outside Early Design Convergence Loop.
- [x] Workflow явно отделяет exploratory discovery от Product Design.
- [x] Outputs не претендуют на durable engineering SoT без later materialization.
- [x] Route to Product Design через bounded initiative clearly defined.
- [x] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [x] `vacancy.md` намеренно не создавались: текущий agreed authoring mode — human-orchestrated draft согласно `human-orchestrated-stage-draft-authoring.md`.
- [x] Links and terminology follow documentation rules.

## Execution Status

- Current State: completed as draft
- Next Step: use the draft workflow on real opportunity discovery work, then formalize only proven routes if needed.
- Blockers: none
- Verification: created workflow-pack files and reviewed draft-mode consistency.

## Handoff

### Completed output

Created draft workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/workflows/opportunity-discovery/
  README.md
  workflow.md
  steps/01-opportunity-signal-intake/STEP.md
  steps/02-problem-and-context-framing/STEP.md
  steps/03-existing-solutions-and-differentiation-scan/STEP.md
  steps/04-opportunity-hypothesis-synthesis/STEP.md
  steps/05-evidence-needs-and-uncertainty-triage/STEP.md
  steps/06-candidate-initiative-shaping/STEP.md
  steps/07-opportunity-routing-decision/STEP.md
```

### Agreed design decisions

- `Opportunity Discovery` is optional and has no fixed top-level SDLC position.
- It can be the first workflow for new project / new horizon / strong redesign exploration, or it can run after / inside `Initiative Workspace Preparation` when human orchestration needs opportunity-level exploration.
- Canonical opportunity workspace root for materialized exploration is `operational_scope/opportunities/<opportunity-slug>/`.
- It answers whether a project/direction/opportunity is worth pursuing and how it may differ from existing solutions.
- It does not prepare iteration workspace for an existing project; that is `Initiative Workspace Preparation` responsibility.
- It does not form Product / Architecture / System image; those are handled by Stage 01 Product Design, Stage 02 Architecture Design and Stage 03 System Design.
- `Existing Solutions and Differentiation Scan` is a key step, but still human-skippable in human-orchestrated execution.
- `Candidate Initiative Shaping` is a separate bridge step before routing decision.
- `vacancy.md` files were intentionally omitted because the current task execution used the newer human-orchestrated draft authoring mode.

### Remaining follow-up outside this task

- Stage 01 Product Design is handled by `wf-021` and another agent.
- Top-level SDLC workflow synchronization with Opportunity Discovery, Initiative Workspace Preparation and Product Design is handled by `wf-022`.
