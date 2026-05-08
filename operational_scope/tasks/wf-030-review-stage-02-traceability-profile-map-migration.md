# Task: Review Stage 02 traceability profile-map migration

## Контекст

This is a critic/review task for the result of:

```text
operational_scope/tasks/wf-029-migrate-stage-02-traceability-profile-to-profile-map.md
```

WF-029 asks an implementation agent to migrate Stage 02 `Architecture Design` traceability profile from a monolithic profile to the reusable `stage-traceability-profile` map + focused guidance structure.

The reviewer must not implement missing scope by default. The reviewer should identify semantic gaps, contradictions, ownership leaks and broken references, then report findings clearly.

## Обязательный reading context

Перед review прочитать:

### Reviewed task

- [`wf-029-migrate-stage-02-traceability-profile-to-profile-map.md`](./wf-029-migrate-stage-02-traceability-profile-to-profile-map.md)

### Pattern and examples

- [`stage-traceability-profile/index.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/stage-traceability-profile/index.md)
- [`templates/`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/stage-traceability-profile/templates/)
- [`product-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/product-traceability-profile.md)
- [`Stage 01 focused traceability docs`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/resources/traceability/)

### Generic and SDLC traceability sources

- [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md)
- [`terms.md`](../../docs/methodology-layer/assets/traceability/terms.md)
- [`traceability-system.md`](../../docs/methodology-layer/assets/traceability/traceability-system.md)
- [`entity-registries.md`](../../docs/methodology-layer/assets/traceability/entity-registries.md)
- [`relationship-and-trace-maps.md`](../../docs/methodology-layer/assets/traceability/relationship-and-trace-maps.md)
- [`trace-chain-type-catalog-decision.md`](../../docs/methodology-layer/assets/traceability/adr/trace-chain-type-catalog-decision.md)
- [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md)
- [`status-semantics.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/status-semantics.md)

### Universal traceability skills

- [`entity-type-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/entity-type-draft-registration/SKILL.md)
- [`relationship-type-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-type-draft-registration/SKILL.md)
- [`entity-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/entity-instance-draft-registration/SKILL.md)
- [`relationship-instance-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/relationship-instance-draft-registration/SKILL.md)
- [`trace-chain-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/skills/trace-chain-draft-registration/SKILL.md)

### Target Stage 02 docs

Review actual state after WF-029 under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/
```

Especially:

- `resources/architecture-traceability-profile.md`;
- `resources/traceability/entity-types.md`;
- `resources/traceability/relationship-types.md`;
- `resources/traceability/entities.md`;
- `resources/traceability/relationships.md`;
- `resources/traceability/trace-chains.md`;
- `workflow.md`;
- `README.md`;
- traceability-related `steps/*/STEP.md`.

## Цель review

Critically verify that Stage 02 profile-map migration is semantically consistent, complete enough for agents, and does not violate Architecture Design ownership boundaries.

## Review focus

Проверить:

### 1. Pattern conformance

- `architecture-traceability-profile.md` works as a short map/routing entrypoint, not a monolithic detailed guide.
- Five focused docs exist under `resources/traceability/`.
- Focused guidance map points to correct files.
- Profile links to `stage-traceability-profile/index.md`.
- Lazy loading / progressive disclosure principle is preserved.

### 2. Layering

- Universal governance stays inside skills.
- Stage 02 focused docs contain Architecture-specific semantics, not duplicated skill algorithms.
- Generic traceability mechanics are not redefined inside Stage 02.
- Stage 02 docs do not introduce project facts or fake project-local catalogs.

### 3. Architecture ownership boundaries

- Architecture Design owns architecture Entity instances only.
- Product/System/Test/task/code Entity definitions are not silently taken by Architecture Design.
- Product/System endpoints are linked only if existing or routed as gaps/handoff notes.
- Contracts/ADRs/key models remain architecture-owned or discoverable through architecture traceability as intended.

### 4. Focused doc quality

- `entity-types.md` has Architecture-owned Entity type candidates and does not define foreign types.
- `relationship-types.md` has Architecture-local relationship semantics with clear directionality and reuse preference.
- `entities.md` has architecture Entity registry guidance, optional detail-page policy and forbidden ownership.
- `relationships.md` has endpoint rules, missing endpoint routing and Relationship type rule.
- `trace-chains.md` has Trace chain prerequisites, cross-domain boundary and no Trace chain type catalog.

### 5. Terminology and status consistency

- Current skill names are used.
- No old names remain:
  - `trace-type-drafter`;
  - `relationship-type-drafter`;
  - `relationship-instance-draft-capture`;
  - `trace-chain-draft-capture`.
- No stray `draft capture` / `draft-capture` wording remains unless explicitly justified.
- Traceability status semantics use `draft`, `provisional`, `active`, `deprecated`.
- No `Trace chain type catalog` is introduced.

### 6. Link and navigation integrity

- Relative links from Stage 02 profile and focused docs resolve.
- Links to pattern, skills, generic traceability asset and SDLC resources are correct.
- Stage 02 workflow/README/steps do not point to deleted skill paths.

## Suggested verification commands

Use grep/read checks equivalent to:

```text
grep old skill names under stages/02-architecture-design
grep "draft capture|draft-capture" under stages/02-architecture-design
grep "Trace chain type catalog" under stages/02-architecture-design
read architecture-traceability-profile.md and each focused doc
compare structure with Stage 01 profile-map implementation
```

## Expected output

Produce a review report with:

- Summary verdict: pass / pass with findings / needs rework.
- Findings grouped by severity:
  - blocking semantic issues;
  - non-blocking inconsistencies;
  - follow-up improvements.
- For each finding:
  - file/path;
  - issue;
  - why it matters;
  - recommended correction.
- Explicit non-findings for major checks that passed.

Do not silently fix implementation unless explicitly requested after the review.

## Definition of Done

- [ ] WF-029 result reviewed against `stage-traceability-profile` pattern.
- [ ] Stage 02 ownership boundaries reviewed.
- [ ] Skill names and deleted paths checked.
- [ ] Trace chain type catalog boundary checked.
- [ ] Link/navigation risks checked.
- [ ] Review report produced with findings and non-findings.

## Execution Status

- Current State: queued
- Next Step: Run after WF-029 implementation is complete.
- Blockers: WF-029 must be completed first.
- Verification: review report only; no implementation changes expected in this task.
