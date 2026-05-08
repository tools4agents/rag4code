# Findings: Stage Traceability Profile critic pass

> Status: Draft  
> Scope: critic pass for `stage-traceability-profile` methodology resource package  
> Target: `assets/metodologes/waterfall/software-development-methodology/resources/traceability/stage-traceability-profile/`

## Проверка 1 — Layering correctness

### Non-findings

- Pattern корректно расположен в methodology layer: `assets/metodologes/waterfall/software-development-methodology/resources/traceability/stage-traceability-profile/`, а не в generic `docs/methodology-layer/assets/traceability/`. Это соответствует layered ownership model из generic `traceability-system.md`: generic asset owns mechanics, methodology profile owns methodology-specific expectations.
- `index.md` явно разделяет ответственность между слоями: generic `traceability-system asset`, SDLC traceability resources, stage profile map, focused stage docs and universal skills.
- Pattern не определяет Product/System/Architecture/Test semantics directly. В `Non-goals` явно сказано, что он не defines Product/System/Architecture/Test semantics, не replaces skills and не defines generic traceability mechanics.
- Pattern не вводит Trace chain type catalog and does not conflict with `trace-chain-type-catalog-decision.md`.

### Findings

No blocking layering findings.

### Risks / assumptions

- Pattern intentionally couples stage profiles to the current set of five universal skills. This is acceptable at the methodology layer, but if the skill set changes later, `stage-traceability-profile/index.md` and templates must be updated together. This should be treated as methodology maintenance, not project-local customization.

## Проверка 2 — Reusability beyond Stage 01

### Non-findings

- Templates mostly use placeholders (`<Domain>`, `Stage <N>`, `<foreign-domain-*>`, `<entity-family-*>`) and do not copy Product-specific candidate lists from Stage 01.
- `index.md` correctly says Stage 01 is a concrete example, not a source of Product-independent semantics.
- Product-specific references in `index.md` are limited to the example implementation and non-goals. That is acceptable for a reusable pattern document.

### Findings

#### Finding 2.1 — Template hardcodes `Design Baseline Consolidation` as promotion owner

- Location: `templates/stage-traceability-profile.template.md`, Shared Stage rules.
- Current text: `Promotion belongs to stage consolidation/review, Design Baseline Consolidation or explicit project-local decision.`
- Issue: this is correct for early design stages, but the pattern is intended for Stage 04 and later SDLC stages too. Later stages may have different consolidation gates or release/execution review flows. Hardcoding `Design Baseline Consolidation` in the reusable template may cause agents to copy an early-design-specific governance route into stages where it is not the correct owner.
- Impact: Stage 04/later profile authors may accidentally route promotion decisions to the wrong consolidation workflow.
- Recommended fix: make the template generic, e.g. `stage consolidation/review, the relevant cross-stage consolidation workflow, or explicit project-local decision`, with a placeholder for stage-specific consolidation owner.

#### Finding 2.2 — Trace chain template hardcodes `Test Design` as a downstream consumer

- Location: `templates/trace-chains.template.md`, `When to create`.
- Current text: `it helps review, handoff, Test Design or consolidation`.
- Issue: `Test Design` is a central downstream consumer for Product/System/Architecture traces, but not necessarily for Stage 04 itself or later execution/release stages. A reusable template should not imply that every stage's Trace chains primarily feed Test Design.
- Impact: later-stage profiles may inherit an incorrect downstream-consumer model.
- Recommended fix: replace with generic wording such as `it helps review, handoff, downstream work or consolidation`, or use `<downstream-consumer>` placeholder.

### Risks / assumptions

- `index.md` says pattern is intended for Stage 02, Stage 03, Stage 04 and later SDLC stages. That is reasonable, but the templates need to stay less early-design-specific than the Stage 01 implementation.

## Проверка 3 — Template safety

### Non-findings

- Templates consistently point to universal skills for mechanics and governance instead of embedding proposal/human-agreement algorithms. This reduces risk of duplicated or divergent governance.
- Templates contain important foreign-domain safety boundaries: no fake foreign Entity IDs, route missing foreign endpoints to handoff/gaps, do not silently decide foreign-domain semantics.
- `relationship-types.template.md` includes directionality and reuse checks, and warns against weak `related-to` semantics.
- `trace-chains.template.md` includes the critical prerequisite rule: Trace chains must be explainable by Relationship instances and must not hide missing Relationship instances.
- `trace-chains.template.md` explicitly says the stage does not introduce Trace chain types or a Trace chain type catalog.

### Findings

#### Finding 3.1 — Template uses `accepted intent`, which can blur status terminology

- Location: `templates/relationship-types.template.md`, `When not to propose`.
- Current text: `semantics are vague, e.g. weak related-to without accepted intent`.
- Issue: after the status terminology migration, `accepted` should not appear as a lifecycle status. Here it is ordinary language, not a row status, but in a template copied by agents it can still blur the distinction between `active` status and human-agreed intent.
- Impact: low. It will not break mechanics, but it weakens terminology cleanliness in a reusable template.
- Recommended fix: replace with `without explicitly agreed intent` or `without clear intended semantics`.

#### Finding 3.2 — Stage profile template omits catalog-routing shared rules present in Stage 01 implementation

- Location: `templates/stage-traceability-profile.template.md`, Shared Stage rules.
- Stage 01 implementation includes shared rules that Entity instances must use Entity types / Entity Identifier families from `entity-type-catalog.md` or route gaps to `entity-type-draft-registration`, and Relationship instances must use Relationship types from `relationship-type-catalog.md` or route gaps to `relationship-type-draft-registration`.
- Issue: focused templates cover parts of this, and skills also enforce it, so this is not a blocker. But the profile map is the routing entrypoint; omitting these two shared rules from the reusable template makes future stage maps weaker than the Stage 01 example and less self-explanatory for agents.
- Impact: future Stage 02/03/04 profiles may omit a useful high-level catalog-gap routing rule even though the pattern expects type skills to exist.
- Recommended fix: add two generic shared rules to the stage profile template:
  - Entity instances must use Entity types and Entity Identifier families from `docs/traceability/entity-type-catalog.md`, or route missing/ambiguous types to `entity-type-draft-registration`.
  - Relationship instances must use Relationship types from `docs/traceability/relationship-type-catalog.md`, or route missing/ambiguous types to `relationship-type-draft-registration`.

### Risks / assumptions

- Template placeholders in angle brackets are clear for humans, but agents may leave placeholders unresolved if the task is rushed. This is a general template-use risk, not a semantic flaw in the pattern.

## Проверка 4 — Lazy loading clarity and skill mapping consistency

### Non-findings

- `index.md` explicitly states a lazy loading order and does not require reading all focused docs for every operation.
- The default skill-to-doc mapping in `index.md` matches `templates/stage-traceability-profile.template.md` and Stage 01 `product-traceability-profile.md`.
- Universal skills now expect stage-local profile/focused guidance where relevant:
  - `entity-type-draft-registration` expects focused Entity type guidance;
  - `relationship-type-draft-registration` expects focused Relationship type guidance;
  - `entity-instance-draft-registration` expects focused Entity registry guidance;
  - `relationship-instance-draft-registration` expects focused relationship guidance;
  - `trace-chain-draft-registration` expects focused trace-chain guidance.

### Findings

#### Finding 4.1 — Lazy loading order puts universal skill instructions last, which can invert execution priority

- Location: `stage-traceability-profile/index.md`, `Lazy loading rule`.
- Current order loads universal skill instructions after catalogs/registries/maps.
- Issue: for an agent executing a skill, universal skill instructions define the operation's governance: proposal-before-write, human agreement, constraints and validation. If the agent reads catalogs/registries before the skill, it may start reasoning about edits before loading the operation contract. This is a small but real operational risk.
- Impact: agents may waste context or miss skill-level constraints during early planning. The risk is higher for type skills because catalog edits are governance-sensitive.
- Recommended fix: change the lazy loading order to load the universal skill before relevant project artifacts, e.g. `STEP.md -> stage profile map -> focused docs -> universal skill -> relevant catalogs/registries/maps`. Keep the note that actual artifact reads should be limited to what the skill and focused doc require.

### Risks / assumptions

- The current order is defensible if the agent already has the skill loaded by the tool/runtime. But as written as human-readable methodology guidance, the safer default is to read the operation contract before the mutable artifacts.

## Проверка 5 — Naming/path portability, handoff/consolidation, status and Trace chain boundary

### Non-findings

- Recommended path `stages/<stage>/resources/<stage-domain>-traceability-profile.md` matches current Stage 01 and likely Stage 02 naming (`product-traceability-profile.md`, `architecture-traceability-profile.md`). It is a recommendation, not a hard project path contract.
- Focused docs use stable, short names that match the five traceability operations.
- Pattern and templates consistently use `draft` and avoid defining `accepted` as a traceability row status.
- Trace chain type boundary is consistently represented: templates say no Trace chain types / no Trace chain type catalog and use `TR-` / `TR-###`.

### Findings

#### Finding 5.1 — Handoff section assumes every stage has downstream stages

- Location: `templates/stage-traceability-profile.template.md`, `Handoff to downstream stages and consolidation`.
- Issue: early SDLC stages naturally hand off to downstream stages, but later stages may hand off to release, verification, operation, maintenance or no further stage. The section title and wording may be too narrow for Stage 04 and later stages.
- Impact: later-stage authors may either keep an awkward section or force downstream-stage semantics where a broader readiness/release/operation handoff model is needed.
- Recommended fix: rename the template section to a more generic `Handoff / readiness / consolidation` or make the heading a placeholder, e.g. `<Handoff/readiness target>`. Keep Stage 01's concrete wording as its implementation-specific version.

#### Finding 5.2 — Recommended profile filename may not fit multi-domain or non-domain stages

- Location: `stage-traceability-profile/index.md`, `Recommended structure`.
- Current text: `stages/<stage>/resources/<stage-domain>-traceability-profile.md`.
- Issue: this fits Product/Architecture/System/Test stages, but later stages may be organized around execution, release, verification, operations or cross-cutting workflows rather than a single domain. `<stage-domain>` can be interpreted too narrowly.
- Impact: low-to-medium. Agents may overfit filenames to a domain concept even when the stage should use a workflow-oriented name.
- Recommended fix: clarify that `<stage-domain>` is a placeholder for the stage-local stable profile name and may be domain-oriented or workflow-oriented, e.g. `<stage-profile-name>-traceability-profile.md`.

### Risks / assumptions

- `Design Baseline Consolidation` and `Test Design` issues are already recorded in Проверка 2. They are also part of handoff/consolidation portability, but not repeated here as separate findings to avoid duplication.

## Проверка 6 — Agent operational usability and semantic gaps in individual templates

### Non-findings

- The package gives a future Stage 02 migration agent enough high-level orientation: pattern `index.md`, templates and Stage 01 example implementation are all present.
- Individual templates are short and focused; they do not become second copies of the universal skills.
- `relationships.template.md` has a useful endpoint model: existing foreign endpoints are allowed only under explicit constraints; missing own-domain and missing foreign-domain endpoints are handled differently.
- `trace-chains.template.md` includes the most important operational guardrail: missing Relationship prerequisites must be visible and routed, not hidden inside a Trace chain row.

### Findings

#### Finding 6.1 — Example implementation paths in `index.md` are not clickable links

- Location: `stage-traceability-profile/index.md`, `Example implementation`.
- Current text lists Stage 01 paths in a plain text block.
- Issue: for an agent or human navigating docs, clickable links reduce lookup friction and make the example easier to inspect. Plain paths are not wrong, but they are less operationally useful.
- Impact: low. The paths are clear, but next-agent task prompts will be cleaner if the pattern itself links to Stage 01 implementation.
- Recommended fix: add a short linked list after the text block, or replace the text block with links to Stage 01 profile and focused docs.

#### Finding 6.2 — `relationships.template.md` omits explicit source/rationale expectation

- Location: `templates/relationships.template.md`.
- Issue: Relationship instances are especially prone to weak or invented links. The universal skill requires source/rationale, but the focused relationship guidance template does not remind the stage author to describe what counts as sufficient source/rationale for this stage.
- Impact: future focused docs may include endpoint rules but omit stage-local evidence/source expectations, making Relationship rows harder to review.
- Recommended fix: add a short `Source/rationale expectations` section to the template, e.g. `Relationship instances should cite the stage output, decision, scenario, model or other source that supports the link.` Keep it stage-specific and avoid duplicating the full skill validation checklist.

#### Finding 6.3 — `relationship-types.template.md` reusable type list omits `implemented-by`

- Location: `templates/relationship-types.template.md`, `Preferred reuse`.
- Issue: The universal skill and SDLC profile include `implemented-by` among typical reusable Relationship types. The template list omits it. For early design this may be harmless, but the pattern is explicitly intended for later stages too, where implementation links become central.
- Impact: later-stage authors may miss an existing canonical Relationship type and draft synonyms for implementation links.
- Recommended fix: add `implemented-by` to the preferred reuse list, or add wording that the list is non-exhaustive and methodology/project catalogs are authoritative.

#### Finding 6.4 — `entities.template.md` does not explicitly route missing Entity type/prefix gaps

- Location: `templates/entities.template.md`.
- Issue: Entity instance registration depends on Entity types and Entity Identifier families. The universal skill handles missing type/prefix gaps, and `entity-types.template.md` covers type drafting, but the focused Entity registry template does not explicitly remind stage authors to route missing own-domain Entity type/prefix gaps to `entity-type-draft-registration`.
- Impact: future stage `entities.md` files may tell agents what Entity instances to register but omit the local type-gap routing bridge.
- Recommended fix: add a short `Entity type rule` section similar to the Relationship type rule in `relationships.template.md`.

### Risks / assumptions

- These are usability gaps rather than architectural blockers. Universal skills still enforce the critical behavior, but the templates can better guide stage-profile authors and future migration agents.

## Итоговая проверка непротиворечивости

### Overall verdict

- Critical blocker не найден: pattern расположен в правильном слое, не смешивает generic asset mechanics with stage semantics, and does not duplicate universal skill governance.
- Main issue class: templates are slightly too early-design-specific and slightly weaker than the Stage 01 implementation in a few routing/source expectation details.
- Findings are mutually consistent: several findings point to the same general improvement direction — make reusable templates more generic for later stages while preserving strong routing and catalog-gap rules.

### Recommended patch priority

1. Fix template portability issues first: Findings 2.1, 2.2, 5.1, 5.2.
2. Fix routing/safety clarity: Findings 3.1, 3.2, 6.2, 6.3, 6.4.
3. Fix operational navigation: Finding 4.1 and 6.1.

### Notes for discussion

- None of the findings require redesigning the pattern package structure.
- The likely patch set is small and localized to `stage-traceability-profile/index.md` and templates.
- Stage 01 implementation can remain as-is; most findings target reusable templates, not the concrete Product Design profile.
