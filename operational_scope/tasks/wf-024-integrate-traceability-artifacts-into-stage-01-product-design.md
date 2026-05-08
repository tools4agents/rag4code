# Task: Integrate traceability artifacts into Stage 01 Product Design

## Контекст

После проектирования generic [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md), SDLC [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md) and `Design Baseline Consolidation` стало видно white spot:

`Stage 01 — Product Design` теперь получает явные steps/guidance для создания and updating traceability artifacts, так как SDLC profile назначает Stage 01 владельцем product Entity registration.

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
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/06-product-entity-registry-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/07-product-relationship-instance-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/08-product-trace-chain-handoff-seed-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/10-product-baseline-materialization/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/11-product-traceability-structural-review/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/12-product-intent-semantic-review-design-routing/STEP.md)
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
- add Product Entity Registry Consolidation, Product Relationship Instance Consolidation, Product Trace Chain & Handoff Seed Consolidation and Product Traceability Structural Review steps;
- update Product Baseline Materialization and Product Intent Semantic Review step docs to mention traceability artifacts;
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

Affected steps:

```text
06-product-entity-registry-consolidation/STEP.md
07-product-relationship-instance-consolidation/STEP.md
08-product-trace-chain-handoff-seed-consolidation/STEP.md
09-product-uncertainty-evidence-routing/STEP.md
10-product-baseline-materialization/STEP.md
11-product-traceability-structural-review/STEP.md
12-product-intent-semantic-review-design-routing/STEP.md
```

## Definition of Done

- [x] Stage 01 docs explicitly say Product Design owns product Entity registration.
- [x] Product Entity registry target `docs/product/entities-map.md` is mentioned.
- [x] Optional product Entity detail page guidance is present.
- [x] Product trace seeds / Relationship handoff guidance is present.
- [x] Stage 01 handoff to Design Baseline Consolidation includes product traceability readiness.
- [x] Boundaries with System Design and Architecture Design remain clear.
- [x] No `vacancy.md` files created under current human-orchestrated draft mode.
- [x] Links to generic traceability asset and SDLC traceability profile are correct.

## Execution Status

- Current State: completed as draft
- Next Step: Use updated Stage 01 traceability steps during Stage 02/03 traceability integration and future Product Design runs.
- Blockers: none
- Verification: read/grep consistency checks for traceability mentions, stale step references and link correctness completed.
