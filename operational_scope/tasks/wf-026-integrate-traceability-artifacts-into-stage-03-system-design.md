# Task: Integrate traceability artifacts into Stage 03 System Design

## Контекст

После проектирования generic [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md), SDLC [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md) and `Design Baseline Consolidation` стало видно white spot:

`Stage 03 — System Design` пока не имеет явных steps/guidance для создания and updating system traceability artifacts, хотя SDLC profile назначает Stage 03 владельцем system Entity registration and Relationship instances from system entities to product entities.

`Design Baseline Consolidation` ожидает system Entity instances, Relationship registry contributions and Trace chain instances before Test Design.

После WF-025 для Stage 02 Architecture Design была принята reusable traceability integration model:

```text
universal skills = reusable traceability mechanics
stage-local traceability profile = domain ownership and boundaries
stage-level steps = consolidation, structural review and semantic routing
Entity / Relationship / Trace Chain work = separated to reduce cognitive load
```

Stage 03 should apply the same model with System-specific ownership and boundaries.

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

### Universal traceability skills

- [`entity-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/entity-instance-draft-registration/SKILL.md)
- [`relationship-instance-draft-capture`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-instance-draft-capture/SKILL.md)
- [`trace-chain-draft-capture`](../../assets/metodologes/waterfall/software-development-methodology/skills/trace-chain-draft-capture/SKILL.md)
- [`trace-type-drafter`](../../assets/metodologes/waterfall/software-development-methodology/skills/trace-type-drafter/SKILL.md)
- [`relationship-type-drafter`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-type-drafter/SKILL.md)

### Target stage and downstream consolidation

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/workflow.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/steps/04-system-level-scenarios-behavior-modeling/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/steps/05-data-state-ownership-framing/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/steps/06-integration-surfaces-external-systems-framing/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/steps/07-operational-constraints-nfr-framing/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/steps/10-system-design-sot-materialization/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/steps/11-system-baseline-review-gate/STEP.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)

### Stage 02 reference implementation

Use Stage 02 as reference pattern, not as content to copy blindly:

- [`architecture-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/resources/architecture-traceability-profile.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/08-architecture-entity-registry-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/09-architecture-relationship-instance-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/10-architecture-trace-chain-contribution-consolidation/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/11-architecture-uncertainty-evidence-routing/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/12-architecture-sot-materialization/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/13-architecture-traceability-structural-review/STEP.md)
- [`STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/steps/14-architecture-baseline-semantic-review-consolidation-routing/STEP.md)

## Цель

Обновить Stage 03 `System Design`, чтобы он явно создавал/обновлял system traceability artifacts according to SDLC traceability profile and the Stage 02 traceability integration pattern.

Нужно определить, где в Stage 03 workflow появляются system Entity instances, product-to-system Relationship instances, architecture-related system Relationships and Trace chain instances, then update relevant workflow/resource/STEP docs.

## Proposed Stage 03 model

Use this target model unless analysis reveals a clear reason to adjust names:

```text
01 System Design Context Intake
02 System Boundary & External Context Framing
03 System Scope & Context Gate
04 System-Level Scenarios & Behavior Modeling
05 Data & State Ownership Framing
06 Integration Surfaces & External Systems Framing
07 Operational Constraints & NFR Framing
08 System Entity Registry Consolidation
09 System Relationship Instance Consolidation
10 System Trace Chain Contribution Consolidation
11 System Uncertainty & Evidence Routing
12 System Design SoT Materialization
13 System Traceability Structural Review
14 System Baseline Semantic Review & Consolidation Routing
```

Expected transformations:

```text
old 08 System Uncertainty Triage + old 09 System Evidence Routing Gate
  -> new 11 System Uncertainty & Evidence Routing

old 10 System Design SoT Materialization
  -> new 12 System Design SoT Materialization

old 11 System Baseline Review Gate
  -> new 14 System Baseline Semantic Review & Consolidation Routing
```

Add new explicit traceability steps:

```text
08 System Entity Registry Consolidation
09 System Relationship Instance Consolidation
10 System Trace Chain Contribution Consolidation
13 System Traceability Structural Review
```

## Scope

Включить:

- create Stage 03 stage-local traceability profile, likely `resources/system-traceability-profile.md`;
- update Stage 03 workflow to use universal traceability skills and the 14-step model;
- add `System Entity Registry Consolidation` step;
- add `System Relationship Instance Consolidation` step;
- add `System Trace Chain Contribution Consolidation` step;
- merge old uncertainty/evidence steps into `System Uncertainty & Evidence Routing`;
- renumber/update `System Design SoT Materialization` as step 12;
- add `System Traceability Structural Review` step;
- rename/expand final gate as `System Baseline Semantic Review & Consolidation Routing`;
- add short traceability hints in working-set steps `04–07` and link to `system-traceability-profile.md`;
- update README and stage-local resources if needed;
- update `human-agreement-rule.md` if it references old gates;
- clarify that System Design owns system Entity registration;
- system Entity families guidance: system design records, system-level scenarios, system behavior records, external actors/systems, integration surfaces, data/state ownership records, runtime modes, system-level NFRs and operational constraints;
- guidance for updating `docs/system_design/entities-map.md`;
- guidance for adding optional `docs/system_design/entities/<entity-id>.md` detail pages when row-level description is insufficient;
- guidance for adding Relationship instances to `docs/traceability/relationships-map.md`, especially links from product requirements/stories/scenarios/acceptance criteria to system behavior/scenarios;
- guidance for contributing Trace chain instances to `docs/traceability/trace-map.md` when system design closes a meaningful product-to-system or product-to-system-to-architecture path;
- guidance to use/request Relationship types from `docs/traceability/relationship-type-catalog.md`;
- clarify that System Design does not own Product/Architecture/Test Entity definitions;
- clarify handoff expectations for Design Baseline Consolidation.

Не включать:

- Product Design entity registry work;
- Architecture Design entity registry work;
- Test Design traceability;
- implementation tasks;
- production code;
- full identifier grammar freeze beyond project/profile guidance;
- new stage-specific mechanics skills;
- new `vacancy.md` files.

## Suggested System traceability profile content

The stage-local profile should define:

- Domain: System;
- Owning stage: Stage 03 `System Design`;
- recommended Entity registry: `docs/system_design/entities-map.md`;
- optional detail pages: `docs/system_design/entities/<entity-id>.md`;
- Relationship registry: `docs/traceability/relationships-map.md`;
- Trace map: `docs/traceability/trace-map.md`;
- allowed system Entity families;
- forbidden ownership: Product, Architecture, Test, task and code Entity definitions;
- Product -> System Relationship rules: allowed only when Product endpoint exists;
- System -> Architecture Relationship rules: allowed only when Architecture endpoint exists and system reasoning supports relation;
- missing Product/Architecture endpoints should become handoff/gaps, not invented IDs;
- universal skill usage and two-stage proposal/agreement/update model;
- handoff expectations for `Design Baseline Consolidation`.

## Typical system Relationship and Trace examples

Relationship examples:

```text
product requirement/story/scenario -> system behavior/scenario
acceptance criterion -> system behavior
system scenario -> external actor
system scenario -> external system
system behavior -> data/state ownership record
system behavior -> integration surface
operational constraint/NFR -> system behavior
system behavior -> architecture context, only if Architecture Entity exists
```

Trace chain examples:

```text
US-003 -> SCN-004 -> SYSSCN-002 -> SYSBEH-005 -> INT-001
REQ-001 -> AC-002 -> SYSBEH-003 -> SNFR-001
US-003 -> SYSBEH-005 -> FLOW-002 -> COMP-004
```

Exact prefixes are project/profile-selected and should not be globally frozen by this task.

## Vacancy handling

Follow the WF-025 vacancy policy:

- do not create new `vacancy.md`;
- if a step is practically unchanged and only renumbered, existing `vacancy.md` may be preserved and renumbered;
- if a step is new, merged from multiple steps, or substantially rewritten, do not create a new vacancy and remove obsolete old vacancy with obsolete step.

## Expected output

Update relevant files under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/03-system-design/
  README.md
  workflow.md
  resources/system-traceability-profile.md
  resources/human-agreement-rule.md, if old gate references exist
  steps/*/STEP.md
```

Expected new or transformed step directories:

```text
08-system-entity-registry-consolidation/
09-system-relationship-instance-consolidation/
10-system-trace-chain-contribution-consolidation/
11-system-uncertainty-evidence-routing/
12-system-design-sot-materialization/
13-system-traceability-structural-review/
14-system-baseline-semantic-review-consolidation-routing/
```

Remove obsolete old step directories only after preserving meaningful content in new steps.

## Definition of Done

- [ ] Stage 03 docs explicitly say System Design owns system Entity registration.
- [ ] Stage 03 uses universal traceability skills instead of stage-specific mechanics skills.
- [ ] `resources/system-traceability-profile.md` exists and defines System domain ownership and boundaries.
- [ ] System Entity registry target `docs/system_design/entities-map.md` is mentioned.
- [ ] Optional system Entity detail page guidance is present.
- [ ] Stage 03 workflow separates Entity / Relationship / Trace Chain consolidation.
- [ ] Product-to-system Relationship contribution guidance is present.
- [ ] System-to-architecture Relationship boundary guidance is present.
- [ ] Trace chain contribution guidance is present.
- [ ] `System Traceability Structural Review` exists and checks structural readiness of system traceability artifacts.
- [ ] Final semantic review checks system baseline and declared traceability before routing to Design Baseline Consolidation.
- [ ] Stage 03 handoff to Design Baseline Consolidation includes system traceability readiness.
- [ ] Boundaries with Product Design, Architecture Design and Test Design remain clear.
- [ ] Old `08/09/10/11` references are updated or removed.
- [ ] Vacancy handling follows WF-025 policy.
- [ ] No new `vacancy.md` files are created.
- [ ] Links to generic traceability asset, traceability terms, SDLC traceability profile and status semantics are correct.

## Execution Status

- Current State: queued
- Next Step: Review Stage 03 current workflow/steps and propose exact file transformation plan before editing.
- Blockers: none
- Verification: read/grep consistency checks for traceability mentions, old step references, link correctness, vacancy handling and Stage 03 14-step completeness.
