# Task: Generalize Stage 01 Product traceability skills to universal SDLC skills

## Контекст

В Stage 01 `Product Design` были созданы workflow-local skills:

- [`product-entity-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/skills/product-entity-draft-registration/SKILL.md)
- [`product-trace-seed-capture`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/skills/product-trace-seed-capture/SKILL.md)

Позже в рамках WF-025 для Stage 02 были созданы universal instance-level traceability skills на уровне methodology package:

- [`entity-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/entity-instance-draft-registration/SKILL.md)
- [`relationship-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-instance-draft-registration/SKILL.md)
- [`trace-chain-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/trace-chain-draft-registration/SKILL.md)

Принята модель:

```text
skills = reusable mechanics
stage workflow / STEP / stage profile = domain-specific ownership and boundaries
stage consolidation/review steps = promotion, structural review, semantic validation
```

Stage 01 local skills теперь частично дублируют universal skills and should be reconciled to avoid maintaining separate Product-specific copies of generic traceability mechanics.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`human-orchestrated-stage-draft-authoring.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/human-orchestrated-stage-draft-authoring.md)

### Traceability assets

- [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md)
- [`terms.md`](../../docs/methodology-layer/assets/traceability/terms.md)
- [`traceability-system.md`](../../docs/methodology-layer/assets/traceability/traceability-system.md)
- [`entity-registries.md`](../../docs/methodology-layer/assets/traceability/entity-registries.md)
- [`relationship-and-trace-maps.md`](../../docs/methodology-layer/assets/traceability/relationship-and-trace-maps.md)
- [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md)
- [`status-semantics.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/status-semantics.md)

### Current universal skills

- [`entity-type-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/entity-type-draft-registration/SKILL.md)
- [`relationship-type-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-type-draft-registration/SKILL.md)
- [`entity-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/entity-instance-draft-registration/SKILL.md)
- [`relationship-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-instance-draft-registration/SKILL.md)
- [`trace-chain-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/trace-chain-draft-registration/SKILL.md)

### Stage 01 Product Design

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/workflow.md)
- [`product-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/product-traceability-profile.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/06-product-entity-registry-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/07-product-relationship-instance-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/08-product-trace-chain-handoff-seed-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/steps/11-product-traceability-structural-review/STEP.md)

### Stage 02 reference implementation

- [`architecture-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/resources/architecture-traceability-profile.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/08-architecture-entity-registry-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/09-architecture-relationship-instance-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/10-architecture-trace-chain-contribution-consolidation/STEP.md)

## Цель

Переработать Stage 01 Product traceability skills so generic traceability mechanics live in universal methodology-level skills, while Product-specific ownership and boundaries are expressed through Stage 01 workflow/steps and a Product traceability profile if needed.

## Scope

Включить:

- analyze overlap between Stage 01 local skills and universal skills;
- decide whether Stage 01 local skills should be removed, deprecated, or converted into thin pointers/wrappers to universal skills;
- add or update Stage 01 product traceability profile if needed, analogous to Stage 02 `architecture-traceability-profile.md` but focused on Product domain;
- update Stage 01 workflow guidance to reference universal skills instead of duplicating mechanics;
- update relevant Stage 01 STEP docs so Product-specific candidate families, ownership boundaries and usage hints live in workflow/steps/profile, not in duplicated skills;
- preserve Product Design boundaries: Stage 01 must not create System/Architecture/Test Entity instances;
- preserve two-stage skill execution model: proposal/human agreement first, artifact update after agreement;
- keep links to `traceability-system terms`, SDLC profile and status semantics correct.

Не включать:

- Stage 02 changes;
- Stage 03/System Design traceability integration;
- Test Design traceability;
- production code;
- implementation tasks;
- full identifier grammar freeze beyond project/profile guidance;
- new `vacancy.md` files.

## Expected output

Update relevant files under:

```text
assets/metodologes/waterfall/software-development-methodology/
  skills/
  stages/01-product-design/
    workflow.md
    resources/*
    steps/*/STEP.md
    skills/*/SKILL.md
```

Likely outcomes:

```text
stages/01-product-design/resources/product-traceability-profile.md
```

and one of:

```text
stages/01-product-design/skills/product-entity-draft-registration/SKILL.md
stages/01-product-design/skills/product-trace-seed-capture/SKILL.md
```

being removed, marked as deprecated/thin wrappers, or replaced by workflow references to universal skills.

Do not create new stage-specific mechanics skills unless analysis shows a clear Product-only behavior that cannot be expressed by universal skills + Product profile + STEP guidance.

## Definition of Done

- [ ] Stage 01 workflow no longer presents Product-specific skills as the primary home of generic Entity/Relationship/Trace capture mechanics.
- [ ] Universal skills are referenced for draft Entity instance registration, Relationship instance capture and Trace chain capture where appropriate.
- [ ] Product-specific ownership and candidate Entity families remain explicit and discoverable.
- [ ] Stage 01 boundaries with System/Architecture/Test remain clear.
- [ ] Existing Stage 01 traceability consolidation/review steps still have enough guidance after local skill generalization.
- [ ] Two-stage proposal/agreement/update mode remains preserved through universal skills.
- [ ] Old Stage 01 local skills are either removed, deprecated, or converted to thin pointers without duplicating generic mechanics.
- [ ] Links to traceability terms, generic traceability asset, SDLC traceability profile and status semantics are correct.
- [ ] No new `vacancy.md` files are created.

## Execution Status

- Current State: completed
- Completed outcome: Stage 01 Product traceability now uses a stage-local `product-traceability-profile.md` plus universal methodology-level traceability skills; old Stage 01 local skill files were removed; Stage 01 steps were split so authoring-time partial capture happens in steps 02–05 and traceability consolidation/review is separated into Entity, Relationship, Trace/Handoff and Structural Review steps.
- Blockers: none
- Verification: grep consistency checks for removed Stage 01 local skill references, universal skill references, product traceability profile references, and absence of new `vacancy.md` files.
