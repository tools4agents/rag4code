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

- [x] WF-029 result reviewed against `stage-traceability-profile` pattern.
- [x] Stage 02 ownership boundaries reviewed.
- [x] Skill names and deleted paths checked.
- [x] Trace chain type catalog boundary checked.
- [x] Link/navigation risks checked.
- [x] Review report produced with findings and non-findings.

## Execution Status

- Current State: completed
- Next Step: Optional follow-up cleanup for non-blocking findings below, if the methodology owner wants stricter profile-map layering.
- Blockers: none.
- Verification: review report only; no implementation changes were made to Stage 02 implementation artifacts during this review.

## Review Report

### Summary verdict

Pass with non-blocking findings.

WF-029 successfully migrated Stage 02 `Architecture Design` traceability profile to the `stage-traceability-profile` map + focused guidance structure. The core ownership model is consistent: Stage 02 owns Architecture Entity instances and architecture-related Relationships/Trace chains, while Product/System/Test/task/code Entity ownership remains outside Stage 02. No blocking semantic issue was found.

The remaining findings are quality/layering improvements, not blockers for accepting the migration.

### Blocking semantic issues

None.

### Non-blocking inconsistencies

#### NBI-1: `workflow.md` still carries a detailed traceability responsibility section that can drift from the new profile-map/focused-doc structure

- File/path: `assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/workflow.md`
- Issue: The workflow still contains a relatively detailed `Architecture traceability responsibility` section with registry locations, Entity families, Relationship/Trace map locations and catalog-gap routing. This overlaps with the new profile map and focused docs.
- Why it matters: The migration's intended structure is: workflow/step context -> short profile map -> operation-specific focused doc -> universal skill. Keeping detailed traceability semantics in `workflow.md` creates a second stage-local source that can diverge from `resources/architecture-traceability-profile.md` and `resources/traceability/*` over time.
- Recommended correction: In a follow-up cleanup, reduce the workflow section to a short routing summary and point readers to `resources/architecture-traceability-profile.md` for map-level boundaries and to `resources/traceability/*` for focused guidance. If the detailed section is intentionally retained as workflow-level summary, mark it explicitly as non-authoritative summary over the profile docs.

### Follow-up improvements

#### FI-1: Some Relationship type examples contain compound alternative semantics in a single row

- File/path: `assets/metodologes/waterfall/software-development-methodology/stages/02-architecture-design/resources/traceability/relationship-types.md`
- Issue: The candidate table uses entries such as `realized by or supported by`, `allocated to or supported by`, and `uses, exposes or is governed by`. These are useful examples, but they combine several possible Relationship meanings in one row.
- Why it matters: Relationship type drafting depends on clear direction and meaning. Compound alternatives can encourage agents to draft or select broad Relationship types instead of choosing one precise existing type or proposing one missing type with explicit semantics.
- Recommended correction: Split compound rows into narrower example rows or add a local rule near the table: agents must choose one precise Relationship meaning from the alternatives and must not draft combined catch-all types.

### Explicit non-findings

- Pattern conformance passed: `architecture-traceability-profile.md` is now a short profile map with source terminology links, domain ownership, focused guidance map, universal skill usage, shared rules and handoff boundaries.
- Five focused docs exist under `resources/traceability/`: `entity-types.md`, `relationship-types.md`, `entities.md`, `relationships.md`, `trace-chains.md`.
- Focused guidance map points to the correct files and follows the Stage 01 profile-map structure.
- The profile links to `stage-traceability-profile/index.md` and preserves lazy loading/progressive disclosure.
- Universal governance is not duplicated as skill algorithms inside Stage 02 focused docs. The docs provide Architecture-specific boundaries, candidates, examples and routing rules.
- Generic traceability mechanics are not redefined by Stage 02. Stage 02 references generic traceability assets, SDLC traceability profile and status semantics instead.
- Architecture ownership boundaries are explicit: Stage 02 may register Architecture Entity instances and architecture-related Relationship/Trace contributions, but must not create Product/System/Test/task/code Entity instances.
- Product/System endpoints are constrained to existing Entity instances or routed as handoff/gaps when missing.
- Contracts, ADRs and key models remain treated as Architecture-owned/discoverable traceability subjects where architecture-significant.
- Current skill names are used: `entity-type-draft-registration`, `relationship-type-draft-registration`, `entity-instance-draft-registration`, `relationship-instance-draft-registration`, `trace-chain-draft-registration`.
- Old skill names were not found under Stage 02: `trace-type-drafter`, `relationship-type-drafter`, `relationship-instance-draft-capture`, `trace-chain-draft-capture`.
- `draft capture` / `draft-capture` wording was not found under Stage 02.
- The Trace chain type catalog boundary is preserved. Mentions of `Trace chain type catalog` under Stage 02 are negative boundary statements, not an introduced catalog.
- Relative links from `architecture-traceability-profile.md` to pattern docs, skills, generic traceability asset, SDLC traceability resources and focused docs resolve at the reviewed paths.
- Stage 02 workflow/README/steps continue to point to the stage-local profile and do not point to deleted skill paths.
