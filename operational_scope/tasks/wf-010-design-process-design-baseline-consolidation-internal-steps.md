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

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/04-test-design/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md)
- [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md)
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
4. не создавать `vacancy.md` в текущем human-orchestrated draft mode;
5. проверить согласованность process workflow, step packs, traceability profile and top-level methodology graph.

## Scope

Включить:

- human-orchestrated internal step model для Design Baseline Consolidation;
- список bounded step vertices and gate-like readiness step;
- happy path and return/remediation guidance;
- intake из Early Design Convergence Loop;
- использование Specification / SoT Materialization для product / architecture / system docs;
- Project Image traceability checks: entity registries, edge map and trace map;
- consistency and non-contradiction review;
- проверку полноты baseline для Test Design;
- white spots, open questions, assumptions and risks triage;
- routing to Research / Deep Research / Spike Experiments;
- readiness decision for Test Design;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` intentionally not included in current human-orchestrated draft mode.

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
  workflow.md                         # updated with human-orchestrated internal steps and step table
  steps/<step-slug>/STEP.md
```

## Definition of Done

- [x] План internal steps обсужден с человеком до создания step packs.
- [x] Согласованный human-orchestrated step model добавлен в `workflows/design-baseline-consolidation/workflow.md`.
- [x] Gate-like readiness decision represented as ordinary draft `STEP.md` guidance according to current authoring mode.
- [x] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [x] `vacancy.md` intentionally not created under current human-orchestrated draft mode.
- [x] Workflow явно фиксирует, что Specification / SoT Materialization не выпускает напрямую в Test Design.
- [x] Workflow проверяет Project Image traceability, consistency, non-contradiction, white spots and readiness for Test Design.
- [x] Links and terminology follow documentation rules for completed draft scope.

## Execution Status

- Current State: completed as draft
- Next Step: Use the workflow on real consolidation work; later formalize stricter gates/vacancies only if practical usage shows they are needed.
- Blockers: none
- Verification: workflow, README and 9 `STEP.md` files created; no `vacancy.md` files by agreed draft mode; grep/read consistency checks only.

## Handoff Notes

- Created human-orchestrated draft steps:
  - `01-consolidation-context-intake`
  - `02-stage-contribution-readiness-intake`
  - `03-entity-registry-readiness-check`
  - `04-cross-domain-edge-map-structural-review`
  - `05-project-image-trace-map-structural-review`
  - `06-cross-baseline-semantic-consistency-review`
  - `07-test-design-input-sufficiency-review`
  - `08-open-questions-white-spots-remediation-routing`
  - `09-test-design-readiness-recommendation`
- Key design decision: traceability structural checks happen before semantic consistency review because they provide the declared Project Image graph for semantic review.
- Design Baseline Consolidation does not repeat deep Product/System/Architecture reviews; it consumes stage-local contribution readiness and owns cross-domain consolidation before Test Design.
- Traceability is modeled through SDLC profile: entity registries, `edges-map.md`, `trace-map.md`, then semantic consistency and Test Design sufficiency.
