# Task: Redesign Stage 01 — Product Design inside Early Design Convergence Loop

## Контекст

Текущий `Stage 01 — Discovery & Intent Framing` противоречиво позиционирован: он одновременно выглядит как preparation/handoff workflow и как vertex внутри Early Design Convergence Loop.

Принято направление: Stage 01 должен стать `Product Design & Intent Framing` — полноценной product-design областью внутри Early Design Convergence Loop. Workspace preparation and exploratory discovery должны быть вынесены в отдельные workflows.

Product Design работает рядом с `Architecture Design` and `System Design`; все три являются design-stage областями, но отвечают за разные concerns:

- Product Design — product intent, value, actors, capabilities, scope, non-goals, usage scenarios, acceptance criteria;
- System Design — system boundary, external context, system-level behavior, data/state ownership, operational constraints;
- Architecture Design — internal components, contracts, runtime flows, key models and decisions.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)

### Current and adjacent stages

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

### Findings and boundary resources

- [`critic_early_design_loop_findings.md`](../findings/critic_early_design_loop_findings.md)
- [`early-design-stage-boundaries.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/early-design-stage-boundaries.md)

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Переделать Stage 01 в `Product Design & Intent Framing` внутри Early Design Convergence Loop.

Нужно:

1. отделить Product Design от workspace preparation and exploratory discovery;
2. добавить entry/re-entry model из Architecture Design and System Design;
3. определить product design core steps;
4. добавить product uncertainty/evidence routing;
5. добавить Product SoT Materialization или clear route through Specification / SoT Materialization;
6. добавить Product Intent Review Gate / baseline readiness gate;
7. согласовать outputs with Stage 02, Stage 03 and Design Baseline Consolidation.

## Scope

Включить:

- new Stage 01 naming and boundary;
- workflow graph with initial entry and focused re-entry;
- step vertices and gate vertices;
- Product Design responsibilities: actors, value, capabilities, responsibilities, scope, non-goals, scenarios, acceptance criteria;
- product-level uncertainty triage;
- human decision and evidence routing;
- SoT materialization rules for product baseline;
- return paths from/to Architecture Design and System Design;
- traceability expectations from product artifacts to system/architecture/test/planning artifacts;
- `STEP.md` для каждого agreed step;
- `vacancy.md` для каждого step pack.

Не включать:

- workspace mechanics except as entry dependency;
- exploratory opportunity discovery;
- system boundary as engineering model;
- internal architecture design;
- test strategy internals;
- implementation task decomposition;
- production code.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- новое имя Stage 01: `Product Design & Intent Framing` или другой вариант;
- какие current Stage 01 steps сохранить, переименовать или вынести;
- какие entry modes нужны: initial from bounded initiative, re-entry from Stage 02, re-entry from Stage 03;
- нужен ли Stage 01 `Lightweight context refresh`, аналогичный Stage 02/03;
- где durable Product SoT: `docs/product/`, `docs/specification/` или project-selected location;
- может ли Stage 02/03 стартовать от operational handoff or only from materialized product baseline;
- какие product baseline verdicts нужны: pass, pass-with-warnings, blocked-research, blocked-probe, human-decision, split, defer, reject.

## Expected output

После выполнения задачи должны появиться или быть обновлены:

```text
assets/metodologes/waterfall/software-development-methodology/stages/01-product-design-intent-framing/
  README.md
  workflow.md
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

Если path migration откладывается, допустимо сначала обновить существующий path:

```text
assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/
```

но задача должна явно зафиксировать migration decision.

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Stage 01 описан как Product Design vertex inside Early Design Convergence Loop.
- [ ] Workspace preparation and Opportunity Discovery removed from Stage 01 core responsibility.
- [ ] Re-entry from Architecture Design and System Design is first-class.
- [ ] Product SoT Materialization / product baseline fixation route defined.
- [ ] Stage 01 boundaries согласованы с `early-design-stage-boundaries.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: обсудить с человеком target Stage 01 graph and migration strategy.
- Blockers: depends on conceptual agreement with tasks `wf-019` and `wf-020`.
- Verification: pending
