# Task: Integrate traceability artifacts into Stage 02 Architecture Design

## Контекст

После проектирования generic [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md), SDLC [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md) and `Design Baseline Consolidation` стало видно white spot:

`Stage 02 — Architecture Design` пока не имеет явных steps/guidance для создания and updating architecture traceability artifacts, хотя SDLC profile назначает Stage 02 владельцем architecture Entity registration and architecture Relationship instances to product/system entities.

`Design Baseline Consolidation` теперь ожидает architecture Entity instances, Relationship registry contributions and Trace chains before Test Design.

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
- [`relationship-and-trace-maps.md`](../../docs/methodology-layer/assets/traceability/relationship-and-trace-maps.md)
- [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md)

### Target stage and downstream consolidation

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/10-architecture-sot-materialization/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/11-architecture-baseline-review-gate/STEP.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

## Цель

Обновить Stage 02 `Architecture Design`, чтобы он явно создавал/обновлял architecture traceability artifacts according to SDLC traceability profile.

Нужно определить, где в Stage 02 workflow появляются architecture Entity instances and cross-domain Relationship instances/Trace chains, and update relevant workflow/STEP docs.

## Scope

Включить:

- architecture Entity families guidance: components, architecture boundaries, runtime flows, contracts, key models, ADRs and durable architecture decisions;
- guidance for updating `docs/architecture/entities-map.md`;
- guidance for architecture-related entities in `docs/contracts/` and `docs/adr/` to remain discoverable from traceability entry points;
- guidance for adding optional `docs/architecture/entities/<entity-id>.md` detail pages when row-level description is insufficient;
- guidance for adding Relationship instances to `docs/traceability/relationships-map.md`, especially links from system behavior/scenarios to components, flows, contracts and ADRs;
- guidance for contributing Trace chains to `docs/traceability/trace-map.md` when architecture closes a meaningful product/system path;
- guidance to use/request Relationship types from `docs/traceability/relationship-type-catalog.md`;
- update Architecture SoT Materialization and/or Architecture Baseline Review Gate docs to mention traceability artifacts;
- clarify that Architecture Design does not own Product/System Entity definitions;
- clarify handoff expectations for Design Baseline Consolidation.

Не включать:

- Product Design entity registry work;
- System Design entity registry work;
- Test Design traceability;
- implementation tasks;
- production code;
- full identifier grammar freeze beyond project/profile guidance;
- `vacancy.md` creation.

## Expected output

Update relevant files under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/
  workflow.md
  steps/*/STEP.md
```

Likely affected steps:

```text
10-architecture-sot-materialization/STEP.md
11-architecture-baseline-review-gate/STEP.md
```

Add new step only if the current step model clearly cannot express traceability responsibilities without overloading existing steps.

## Definition of Done

- [ ] Stage 02 docs explicitly say Architecture Design owns architecture Entity registration.
- [ ] Architecture Entity registry target `docs/architecture/entities-map.md` is mentioned.
- [ ] Contract/ADR discoverability through traceability entry points is clarified.
- [ ] Optional architecture Entity detail page guidance is present.
- [ ] Architecture Relationship/Trace contribution guidance is present.
- [ ] Stage 02 handoff to Design Baseline Consolidation includes architecture traceability readiness.
- [ ] Boundaries with Product Design and System Design remain clear.
- [ ] No `vacancy.md` files created under current human-orchestrated draft mode.
- [ ] Links to generic traceability asset and SDLC traceability profile are correct.

## Execution Status

- Current State: queued
- Next Step: Review Stage 02 materialization/review steps and update them with architecture traceability responsibilities.
- Blockers: none
- Verification: read/grep consistency checks for traceability mentions and link correctness.
