# Task: Migrate traceability terminology to Entity / Relationship model

## Контекст

Во время работы над [`wf-024`](./wf-024-integrate-traceability-artifacts-into-stage-01-product-design.md) и generic [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md) была выявлена терминологическая несогласованность.

Текущие traceability docs and templates часто используют graph-technical wording:

```text
edge / edges-map.md / relationship label
```

Но agreed semantic model для traceability должен быть file-first and meaning-first:

```text
Entity / Entity type / Entity instance
Relationship / Relationship type / Relationship instance
Trace chain / Trace chain instance
```

Graph remains derived projection, not Source of Truth. Поэтому в traceability docs нужно по смыслу оперировать `Entity`, `Relationship` and `Trace chain`, а technical graph terms использовать только в graph projection / implementation context.

## Решения, которые уже согласованы

### Entity terminology

Использовать такую модель:

- `Entity` — понятие Сущности в целом.
- `Entity instance` — конкретная Сущность with stable ID.
- `Entity type` — тип Сущности.
- `Entity Identifier family` — правило / pattern создания уникальных IDs для Entity instances. Обычно связано с Entity type (`REQ-`, `US-`, `SCN-`, `ADR-`, `TC-`) and ordinal number, но project may define its own identifier rules.
- `Entity type catalog` — catalog of Entity types and identifier families.
- `Entity registry` — registry of Entity instances.

Technical mapping only for graph projection context:

```text
Entity instance -> graph vertex
```

### Relationship terminology

Использовать симметричную модель:

- `Relationship` — понятие связи между Entity в целом.
- `Relationship instance` — конкретная связь между двумя Entity instances. Может иметь ID в будущем, но сейчас не усложняем.
- `Relationship type` — тип связи между Entity, e.g. `details`, `realizes`, `supports`, `constrains`, `verifies`.
- `Relationship type catalog` — catalog of Relationship types.
- `Relationship registry` — registry of Relationship instances.

Technical mapping only for graph projection context:

```text
Relationship instance -> graph edge
```

### Trace terminology

Использовать такую модель:

- `Trace chain` — понятие meaningful path over Relationships.
- `Trace chain instance` — конкретный trace chain with unique `Trace ID`.
- `Trace Identifier family` — one family for trace chain instances, default `TR-`.
- `Trace map` / `Trace chain registry` — registry of Trace chain instances.

Не вводить `Trace chain type` сейчас. Если после практического использования появятся устойчивые кластеры trace chains, их можно выделить отдельной задачей.

Technical mapping only for graph projection context:

```text
Trace chain instance -> curated graph path over Relationship instances
```

### File naming decision

Зафиксировать semantic naming:

```text
docs/traceability/relationships-map.md
```

instead of:

```text
docs/traceability/edges-map.md
```

Также заменить semantic concept:

```text
relationship-label-catalog.md -> relationship-type-catalog.md
```

because catalog stores Relationship types, not merely labels.

The project has not yet materialized real traceability catalogs in downstream projects, so it is better to migrate methodology/assets now before wrong terminology becomes project-local practice.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Generic traceability asset

- [`traceability-system asset`](../../docs/methodology-layer/assets/traceability/index.md)
- [`terms.md`](../../docs/methodology-layer/assets/traceability/terms.md)
- [`traceability-system.md`](../../docs/methodology-layer/assets/traceability/traceability-system.md)
- [`entity-registries.md`](../../docs/methodology-layer/assets/traceability/entity-registries.md)
- [`relationship-and-trace-maps.md`](../../docs/methodology-layer/assets/traceability/relationship-and-trace-maps.md)
- [`graph-projection.md`](../../docs/methodology-layer/assets/traceability/graph-projection.md)
- [`resources/`](../../docs/methodology-layer/assets/traceability/resources/)

### SDLC traceability methodology

- [`sdlc-traceability-profile.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/traceability/sdlc-traceability-profile.md)
- [`resource-placement-guidelines.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/resource-placement-guidelines.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/workflow.md)
- Design Baseline Consolidation steps:
  - [`03 Entity Registry Readiness Check`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/steps/03-entity-registry-readiness-check/STEP.md)
  - [`04 Cross-Domain Relationship Registry Structural Review`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/steps/04-cross-domain-relationship-registry-structural-review/STEP.md)
  - [`05 Project Image Trace Map Structural Review`](../../assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/steps/05-project-image-trace-map-structural-review/STEP.md)

### Stage 01 traceability skills already created

- [`product-entity-draft-registration`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/skills/product-entity-draft-registration/SKILL.md)
- [`product-trace-seed-capture`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/skills/product-trace-seed-capture/SKILL.md)

## Цель

Мигрировать generic traceability asset and SDLC traceability methodology docs from graph-technical `edge/label` terminology to semantic `Relationship / Relationship type / Relationship instance` terminology.

Нужно, чтобы future agents and humans used one consistent model:

```text
Entity instance is technically graph vertex.
Relationship instance is technically graph edge.
Trace chain instance is technically curated graph path.

But traceability docs use Entity / Relationship / Trace chain by default.
Graph terms are used only in graph projection / technical implementation context.
```

## Scope

Включить:

- update `docs/methodology-layer/assets/traceability/terms.md` according to agreed model;
- replace confusing standalone `Relationship label` terminology with `Relationship type`; if `label` is mentioned, describe it only as stored representation of Relationship type value;
- rename conceptual references:
  - `edge map` -> `relationship map` or `Relationship registry`;
  - `edges-map.md` -> `relationships-map.md`;
  - `relationship-label-catalog.md` -> `relationship-type-catalog.md`;
- update generic traceability docs:
  - `index.md`;
  - `traceability-system.md`;
  - `entity-registries.md`;
  - `edge-and-trace-maps.md` or rename/reframe it if appropriate;
  - `graph-projection.md`;
- update generic traceability templates under `docs/methodology-layer/assets/traceability/resources/`;
- update SDLC traceability profile under `assets/metodologes/waterfall/software-development-methodology/resources/traceability/`;
- update Design Baseline Consolidation workflow and steps to check Relationship registry / Relationship instances instead of edge map wording;
- update Stage 01 Product Design skills created in this session so they request missing Relationship types and write relationship seeds/instances consistently;
- update pending traceability tasks `wf-024`, `wf-025`, `wf-026` if their wording still references `edges-map.md` or relationship labels as canonical current terminology;
- run grep checks for stale terminology.

Не включать:

- production code;
- graph database implementation;
- MCP contract changes;
- changing actual downstream project traceability files outside methodology/assets, because no project-specific traceability instance exists yet;
- adding `Edge ID` or mandatory `Relationship instance ID`;
- adding `Trace chain type` taxonomy;
- full identifier grammar freeze beyond project/profile guidance;
- `vacancy.md` creation.

## Important terminology guidance for execution

Use this distinction consistently:

```text
Entity = concept of entity.
Entity instance = concrete entity with ID.
Entity type = type/family of entity.
Entity Identifier family = project-defined ID family/pattern for entity instances.
Entity type catalog = catalog of entity types and identifier families.
Entity registry = registry of entity instances.

Relationship = concept of relationship between entities.
Relationship instance = concrete relationship between two entity instances.
Relationship type = type of relationship, e.g. details/realizes/supports.
Relationship type catalog = catalog of relationship types.
Relationship registry / relationships-map.md = registry of relationship instances.

Trace chain = concept of meaningful path over relationships.
Trace chain instance = concrete trace chain with Trace ID.
Trace Identifier family = TR-.
Trace map = registry of Trace chain instances.
```

Technical graph terminology should be restricted:

```text
Entity instance -> vertex only in graph projection context.
Relationship instance -> edge only in graph projection context.
Trace chain instance -> curated graph path only in graph projection context.
```

## Expected output

Update relevant files under:

```text
docs/methodology-layer/assets/traceability/
assets/metodologes/waterfall/software-development-methodology/resources/traceability/
assets/metodologes/waterfall/software-development-methodology/workflows/design-baseline-consolidation/
assets/metodologes/waterfall/software-development-methodology/stages/01-product-design/skills/
operational_scope/tasks/wf-024-integrate-traceability-artifacts-into-stage-01-product-design.md
operational_scope/tasks/wf-025-integrate-traceability-artifacts-into-stage-02-architecture-design.md
operational_scope/tasks/wf-026-integrate-traceability-artifacts-into-stage-03-system-design.md
```

If a file rename is performed, preserve links and update all references.

## Suggested grep checks

Run fresh searches and update stale current terminology where appropriate:

```text
edges-map.md
edge map
Edge map
edge-and-trace
relationship-label-catalog.md
relationship label
Relationship label
label catalog
atomic edges
graph edges
```

Do not remove graph terms from graph projection / technical implementation context; only remove them from semantic traceability concepts where `Relationship` should be used.

## Definition of Done

- [x] Generic traceability terms define `Entity / Entity instance / Entity type` and `Relationship / Relationship instance / Relationship type` symmetrically.
- [x] `Relationship label` is no longer a separate semantic concept; if mentioned, it is only stored representation of a Relationship type value.
- [x] `relationships-map.md` is the canonical semantic filename for Relationship registry in docs/templates/profile.
- [x] `relationship-type-catalog.md` is the canonical semantic filename for Relationship type catalog in docs/templates/profile.
- [x] `edges-map.md` no longer appears as current canonical semantic traceability registry outside explicit legacy/migration notes or graph projection context.
- [x] Design Baseline Consolidation checks Relationship registry / Relationship instances terminology.
- [x] Stage 01 traceability skills use Relationship terminology and request `relationship-type-drafter` when a needed Relationship type is missing.
- [x] Pending tasks `wf-024`–`wf-026` are synchronized with new filenames/terminology.
- [x] Graph projection docs still explain technical mapping Entity -> vertex, Relationship -> edge, Trace chain -> path.
- [x] Links are correct after any file rename.

## Execution Status

- Current State: completed
- Next Step: Use `relationships-map.md` / `relationship-type-catalog.md` terminology in follow-up Stage 02/03 traceability integration tasks.
- Blockers: none
- Verification: grep checks listed above plus link/path review after renames completed; remaining legacy terms are in this migration task historical scope or explicit graph projection context.
