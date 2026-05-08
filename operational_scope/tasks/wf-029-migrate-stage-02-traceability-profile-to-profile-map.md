# Task: Migrate Stage 02 traceability profile to profile-map pattern

## Контекст

Stage 02 `Architecture Design` already references current universal traceability skills:

- `entity-type-draft-registration`;
- `relationship-type-draft-registration`;
- `entity-instance-draft-registration`;
- `relationship-instance-draft-registration`;
- `trace-chain-draft-registration`.

However, Stage 02 still uses older monolithic traceability profile structure in:

```text
assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/resources/architecture-traceability-profile.md
```

Stage 01 `Product Design` now implements reusable `stage-traceability-profile` pattern:

```text
resources/<stage-traceability-profile>.md
resources/traceability/
  entity-types.md
  relationship-types.md
  entities.md
  relationships.md
  trace-chains.md
```

The methodology now has a reusable pattern and templates under:

```text
assets/metodologes/waterfall/software-development-methodology/resources/traceability/stage-traceability-profile/
```

Stage 02 should migrate to the same map + focused guidance structure to reduce cognitive load and make future Stage 03/04 migrations consistent.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`human-orchestrated-stage-draft-authoring.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/human-orchestrated-stage-draft-authoring.md)

### Traceability assets and SDLC profile

- [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md)
- [`terms.md`](../../docs/methodology-layer/assets/traceability/terms.md)
- [`traceability-system.md`](../../docs/methodology-layer/assets/traceability/traceability-system.md)
- [`entity-registries.md`](../../docs/methodology-layer/assets/traceability/entity-registries.md)
- [`relationship-and-trace-maps.md`](../../docs/methodology-layer/assets/traceability/relationship-and-trace-maps.md)
- [`trace-chain-type-catalog-decision.md`](../../docs/methodology-layer/assets/traceability/adr/trace-chain-type-catalog-decision.md)
- [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md)
- [`status-semantics.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/status-semantics.md)

### Stage traceability profile pattern

- [`stage-traceability-profile/index.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/stage-traceability-profile/index.md)
- [`templates/`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/stage-traceability-profile/templates/)

### Universal traceability skills

- [`entity-type-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/entity-type-draft-registration/SKILL.md)
- [`relationship-type-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-type-draft-registration/SKILL.md)
- [`entity-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/entity-instance-draft-registration/SKILL.md)
- [`relationship-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-instance-draft-registration/SKILL.md)
- [`trace-chain-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/trace-chain-draft-registration/SKILL.md)

### Stage 01 example implementation

Use Stage 01 as structural example, not as Product semantics to copy:

- [`product-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/product-traceability-profile.md)
- [`entity-types.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/traceability/entity-types.md)
- [`relationship-types.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/traceability/relationship-types.md)
- [`entities.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/traceability/entities.md)
- [`relationships.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/traceability/relationships.md)
- [`trace-chains.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/traceability/trace-chains.md)

### Target Stage 02 docs

- [`architecture-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/resources/architecture-traceability-profile.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/README.md)
- Stage 02 traceability-related steps:
  - [`08 Architecture Entity Registry Consolidation`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/08-architecture-entity-registry-consolidation/STEP.md)
  - [`09 Architecture Relationship Instance Consolidation`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/09-architecture-relationship-instance-consolidation/STEP.md)
  - [`10 Architecture Trace Chain Contribution Consolidation`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/10-architecture-trace-chain-contribution-consolidation/STEP.md)
  - [`13 Architecture Traceability Structural Review`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/13-architecture-traceability-structural-review/STEP.md)

## Цель

Migrate Stage 02 `Architecture Design` traceability profile to the reusable `stage-traceability-profile` map + focused guidance structure while preserving Architecture-specific ownership and boundaries.

## Scope

Включить:

- convert `resources/architecture-traceability-profile.md` into a stable profile map;
- add focused docs under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/resources/traceability/
  entity-types.md
  relationship-types.md
  entities.md
  relationships.md
  trace-chains.md
```

- preserve Architecture ownership semantics:
  - Architecture Design owns architecture Entity instances;
  - Architecture Design does not own Product/System/Test/task/code Entity definitions unless explicitly scoped;
  - needed Product/System endpoints must exist or be recorded as gaps/handoff notes;
- move Architecture-specific detailed guidance from monolithic profile into focused docs;
- keep universal governance inside skills and do not duplicate skill algorithms in focused docs;
- ensure `architecture-traceability-profile.md` links to `stage-traceability-profile/index.md`;
- ensure focused docs reference correct universal skill names;
- preserve guidance for Architecture Entity families such as architecture components, boundaries, runtime flows, contracts, key models, ADRs and durable architecture decisions;
- preserve guidance for Relationship instances from system/product context to architecture components, flows, contracts and ADRs;
- preserve Trace chain contribution guidance for meaningful architecture paths;
- preserve handoff expectations for `Design Baseline Consolidation`.

Не включать:

- migrating Stage 03 or Stage 04;
- changing universal skills;
- changing generic `traceability-system asset`;
- changing Stage 01 files except if a broken link is found and must be reported;
- introducing Trace chain type catalog;
- production code;
- `vacancy.md` creation;
- full identifier grammar freeze beyond project/profile guidance.

## Expected output

Updated or new files under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/
  resources/architecture-traceability-profile.md
  resources/traceability/entity-types.md
  resources/traceability/relationship-types.md
  resources/traceability/entities.md
  resources/traceability/relationships.md
  resources/traceability/trace-chains.md
  workflow.md                       # only if references need updating
  README.md                         # only if references need updating
  steps/*/STEP.md                   # only if references need updating
```

## Definition of Done

- [ ] `architecture-traceability-profile.md` is a profile map, not a monolithic detailed guidance document.
- [ ] Stage 02 has five focused docs under `resources/traceability/`.
- [ ] Focused docs contain Architecture-specific boundaries, candidates, examples and routing rules.
- [ ] Focused docs do not duplicate universal skill governance/algorithms.
- [ ] Architecture ownership boundaries remain explicit and correct.
- [ ] Product/System/Test/task/code ownership is not silently taken by Architecture Design.
- [ ] Universal skill names are current:
  - `entity-type-draft-registration`;
  - `relationship-type-draft-registration`;
  - `entity-instance-draft-registration`;
  - `relationship-instance-draft-registration`;
  - `trace-chain-draft-registration`.
- [ ] No old skill names remain under Stage 02:
  - `trace-type-drafter`;
  - `relationship-type-drafter`;
  - `relationship-instance-draft-capture`;
  - `trace-chain-draft-capture`.
- [ ] No `draft capture` / `draft-capture` wording remains under Stage 02 traceability docs unless there is explicit rationale.
- [ ] No Trace chain type catalog is introduced.
- [ ] Links to pattern, skills, generic traceability asset and SDLC traceability resources are correct.
- [ ] Report changed files and unresolved semantic questions, if any.

## Execution Status

- Current State: queued
- Next Step: Assign to implementation agent, then run independent critical review against Stage 01 pattern and Stage 02 ownership boundaries.
- Blockers: none known.
- Verification: grep old skill names/draft-capture wording under Stage 02; read profile map and focused docs for layering and ownership consistency.
