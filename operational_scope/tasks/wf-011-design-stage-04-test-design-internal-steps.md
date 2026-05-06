# Task: Design Stage 04 — Test Design internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stage workflows и process workflows.

`Stage 04 — Test Design` уже имеет stage workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/
  README.md
  workflow.md
```

Этот stage идет после process workflow `Design Baseline Consolidation` и до process workflow `Pre-Planning Baseline Freeze`:

```text
Design Baseline Consolidation
  -> Test Design
  -> Pre-Planning Baseline Freeze
```

`Test Design` проектирует testing system: как проверять expected behavior системы, как быстро видеть regressions и как связывать tests с product intent, system design, architecture and contracts.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target stage

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/pre-planning-baseline-freeze/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`test-map.md`](../../docs/methodology-layer/assets/testing-system/test-map.md)
- [`test-suites.md`](../../docs/methodology-layer/assets/testing-system/test-suites.md)
- [`test-case-traceability.md`](../../docs/methodology-layer/assets/testing-system/test-case-traceability.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)
- [`rules-documentation`](../../assets/rules/rules-documentation)

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Проработать internal steps для `Stage 04 — Test Design` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в stage `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность stage workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- Test Design internal workflow graph;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- intake из Design Baseline Consolidation;
- design of unit test boundaries;
- design of integration test boundaries;
- design of critical e2e scenarios;
- optional contract, UI, visual, smoke, regression, performance, security, migration, compatibility, property-based and golden/snapshot tests;
- testing strategy and test-map expectations;
- traceability from product/system/architecture/contracts to tests;
- handling of test design gaps that return to Architecture Design, System Design or Product Design;
- readiness output for Pre-Planning Baseline Freeze;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- implementation of tests;
- execution of verification checks;
- Integration & Verification internals;
- full task decomposition;
- production code;
- release or cleanup logic.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие test design steps являются обязательными, а какие optional;
- как разделить unit, integration and e2e responsibilities;
- как избежать inverted test pyramid;
- где проектировать contract tests;
- где проектировать UI tests, например Playwright visual checks или Storybook-based component/UI checks;
- как test design должен выявлять gaps в architecture, system behavior or product scenarios;
- какой readiness gate нужен перед Pre-Planning Baseline Freeze;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `stages/04-test-design/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Workflow покрывает required baseline: unit, integration and e2e.
- [ ] Optional test types описаны как conditional, а не mandatory для всех проектов.
- [ ] Workflow может вернуть gaps в Architecture Design, System Design, Product Design или Research/Spike.
- [ ] Stage workflow не требует hidden knowledge from `operational_scope/` as SoT.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Test Design.
- Blockers: none
- Verification: Проверить stage workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.
