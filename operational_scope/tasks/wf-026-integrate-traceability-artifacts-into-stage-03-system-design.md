# Task: Integrate traceability artifacts into Stage 03 System Design

## Контекст

После проектирования generic [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md), SDLC [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md) and `Design Baseline Consolidation` стало видно white spot:

`Stage 03 — System Design` пока не имеет явных steps/guidance для создания and updating system traceability artifacts, хотя SDLC profile назначает Stage 03 владельцем system entity registration and links from system entities to product entities.

`Design Baseline Consolidation` теперь ожидает system entities, edge map contributions and trace seeds before Test Design.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`human-orchestrated-stage-draft-authoring.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/human-orchestrated-stage-draft-authoring.md)

### Traceability assets

- [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md)
- [`traceability-system.md`](../../docs/methodology-layer/assets/traceability/traceability-system.md)
- [`entity-registries.md`](../../docs/methodology-layer/assets/traceability/entity-registries.md)
- [`edge-and-trace-maps.md`](../../docs/methodology-layer/assets/traceability/edge-and-trace-maps.md)
- [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md)

### Target stage and downstream consolidation

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/steps/10-system-design-sot-materialization/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/steps/11-system-baseline-review-gate/STEP.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

## Цель

Обновить Stage 03 `System Design`, чтобы он явно создавал/обновлял system traceability artifacts according to SDLC traceability profile.

Нужно определить, где в Stage 03 workflow появляются system entities and product-to-system edges, and update relevant workflow/STEP docs.

## Scope

Включить:

- system entity families guidance: system design records, system-level scenarios, external actors/systems, integration surfaces, data/state ownership records, system-level NFRs and operational constraints;
- guidance for updating `docs/system_design/entities-map.md`;
- guidance for adding optional `docs/system_design/entities/<entity-id>.md` detail pages when row-level description is insufficient;
- guidance for adding edges to `docs/traceability/edges-map.md`, especially links from product requirements/stories/scenarios/acceptance criteria to system behavior/scenarios;
- guidance for contributing trace seeds/chains to `docs/traceability/trace-map.md` when system design closes a meaningful product-to-system path;
- update System Design SoT Materialization and/or System Baseline Review Gate docs to mention traceability artifacts;
- clarify that System Design does not own Product/Architecture entity definitions;
- clarify handoff expectations for Design Baseline Consolidation.

Не включать:

- Product Design entity registry work;
- Architecture Design entity registry work;
- Test Design traceability;
- implementation tasks;
- production code;
- full identifier grammar freeze beyond project/profile guidance;
- `vacancy.md` creation.

## Expected output

Update relevant files under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/
  workflow.md
  steps/*/STEP.md
```

Likely affected steps:

```text
10-system-design-sot-materialization/STEP.md
11-system-baseline-review-gate/STEP.md
```

Add new step only if the current step model clearly cannot express traceability responsibilities without overloading existing steps.

## Definition of Done

- [ ] Stage 03 docs explicitly say System Design owns system entity registration.
- [ ] System entity registry target `docs/system_design/entities-map.md` is mentioned.
- [ ] Optional system entity detail page guidance is present.
- [ ] Product-to-system edge/trace contribution guidance is present.
- [ ] Stage 03 handoff to Design Baseline Consolidation includes system traceability readiness.
- [ ] Boundaries with Product Design and Architecture Design remain clear.
- [ ] No `vacancy.md` files created under current human-orchestrated draft mode.
- [ ] Links to generic traceability asset and SDLC traceability profile are correct.

## Execution Status

- Current State: queued
- Next Step: Review Stage 03 materialization/review steps and update them with system traceability responsibilities.
- Blockers: none
- Verification: read/grep consistency checks for traceability mentions and link correctness.
