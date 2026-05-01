# Task: Design process workflow — Design Baseline Consolidation internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stage workflows и process workflows.

`Design Baseline Consolidation` уже имеет process workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/
  README.md
  workflow.md
```

Этот workflow расположен между Early Design Convergence Loop и `Stage 04 — Test Design`.

Его задача — не просто выполнить gate, а провести процесс фиксации и проверки текущего product / architecture / system baseline перед Test Design:

```text
Early Design Convergence Loop
  -> Design Baseline Consolidation
  -> Test Design
```

Specification / SoT Materialization может закреплять отдельные части договоренностей в `docs/`, но не выпускает напрямую в Test Design. Переход к Test Design разрешает только `Design Baseline Consolidation`.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target process workflow

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
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

Проработать internal steps для process workflow `Design Baseline Consolidation` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в process `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность process workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- internal workflow graph для Design Baseline Consolidation;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- intake из Early Design Convergence Loop;
- использование Specification / SoT Materialization для product / architecture / system docs;
- consistency and non-contradiction review;
- проверку полноты baseline для Test Design;
- white spots, open questions, assumptions and risks triage;
- routing to Research / Deep Research / Spike Experiments;
- readiness decision for Test Design;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- Test Design internal steps;
- full implementation-ready SoT freeze;
- implementation plan cleanup;
- task decomposition;
- production code;
- release or cleanup logic.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие checks обязательны перед Test Design;
- что значит “baseline enough for Test Design”, но еще не full implementation-ready SoT;
- как отличать blocker, warning and known risk;
- нужен ли отдельный step для SoT materialization intake;
- нужен ли отдельный critic/review step;
- как фиксировать contradictions and white spots;
- какие verdicts должен иметь readiness gate;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `workflows/design-baseline-consolidation/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Workflow явно фиксирует, что Specification / SoT Materialization не выпускает напрямую в Test Design.
- [ ] Workflow проверяет consistency, non-contradiction, white spots and readiness for Test Design.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Design Baseline Consolidation.
- Blockers: none
- Verification: Проверить process workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.
