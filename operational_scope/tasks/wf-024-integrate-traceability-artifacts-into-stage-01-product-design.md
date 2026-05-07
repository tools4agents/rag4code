# Task: Integrate traceability artifacts into Stage 01 Product Design

## Контекст

После проектирования generic [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md), SDLC [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md) and `Design Baseline Consolidation` стало видно white spot:

`Stage 01 — Product Design` пока не имеет явных steps/guidance для создания and updating traceability artifacts, хотя SDLC profile назначает Stage 01 владельцем product Entity registration.

`Design Baseline Consolidation` теперь ожидает, что Product Design contribution может предоставить product Entity instances and trace seeds before cross-domain consolidation.

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

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/workflow.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/06-product-baseline-materialization/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/07-product-intent-review-design-routing/STEP.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

## Цель

Обновить Stage 01 `Product Design`, чтобы он явно создавал/обновлял product traceability artifacts according to SDLC traceability profile.

Нужно определить, где в Stage 01 workflow появляются product Entity instances and product trace seeds, and update relevant workflow/STEP docs.

## Scope

Включить:

- product Entity families guidance: requirements, product capabilities, user stories, user scenarios, acceptance criteria and product-level assumptions/risks when stable references are needed;
- guidance for updating `docs/product/entities-map.md`;
- guidance for adding optional `docs/product/entities/<entity-id>.md` detail pages when row-level description is insufficient;
- guidance for contributing product-local Relationship instances to `docs/traceability/relationships-map.md` or downstream trace seeds as handoff notes when downstream Entity instances do not exist yet;
- guidance to use/request Relationship types from `docs/traceability/relationship-type-catalog.md`;
- update Product Baseline Materialization and/or Product Intent Review step docs to mention traceability artifacts;
- clarify that Product Design does not own System/Architecture Entity instances;
- clarify handoff expectations for Design Baseline Consolidation.

Не включать:

- System Design entity registry work;
- Architecture Design entity registry work;
- Test Design traceability;
- implementation tasks;
- production code;
- full identifier grammar freeze beyond project/profile guidance;
- `vacancy.md` creation.

## Expected output

Update relevant files under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/
  workflow.md
  steps/*/STEP.md
```

Likely affected steps:

```text
06-product-baseline-materialization/STEP.md
07-product-intent-review-design-routing/STEP.md
```

Add new step only if the current step model clearly cannot express traceability responsibilities without overloading existing steps.

## Definition of Done

- [ ] Stage 01 docs explicitly say Product Design owns product Entity registration.
- [ ] Product Entity registry target `docs/product/entities-map.md` is mentioned.
- [ ] Optional product Entity detail page guidance is present.
- [ ] Product trace seeds / Relationship handoff guidance is present.
- [ ] Stage 01 handoff to Design Baseline Consolidation includes product traceability readiness.
- [ ] Boundaries with System Design and Architecture Design remain clear.
- [ ] No `vacancy.md` files created under current human-orchestrated draft mode.
- [ ] Links to generic traceability asset and SDLC traceability profile are correct.

## Execution Status

- Current State: queued
- Next Step: Review Stage 01 materialization/review steps and update them with product traceability responsibilities.
- Blockers: none
- Verification: read/grep consistency checks for traceability mentions and link correctness.
