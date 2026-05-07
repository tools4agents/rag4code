# Entity Registries

> Status: Draft  
> Scope: Entity registry pattern внутри `traceability-system asset`  
> Role: Source of Truth для maps of Entity instances

## Назначение

Entity registry — это реестр Entity instances проекта, которые должны быть findable by agents and extractable into derived graph projection.

Главная идея:

```text
terms-map registers terms
entities-map registers project Entity instances
```

In graph projection context, Entity instances become graph vertices. In traceability SoT docs use Entity terminology by default.

## Baseline layout

Recommended domain-local layout:

```text
docs/<domain>/
  entities-map.md
  entities/
    <entity-id>.md
```

`entities-map.md` является primary entrypoint для domain Entity instances. Detail pages are optional and used for large, high-impact or frequently referenced entities.

## Entity map baseline columns

Recommended minimum table:

```markdown
| ID | Type | Name | Short meaning | Detail page | Status |
| --- | --- | --- | --- | --- | --- |
| ENT-001 | example-type | Example entity | Short explanation. | [`ENT-001`](./entities/ENT-001.md) | accepted |
```

Recommended columns:

- `ID` — stable Entity identifier;
- `Type` — domain or methodology-specific Entity type;
- `Name` — human-readable name;
- `Short meaning` — concise agent-readable explanation;
- `Detail page` — optional link;
- `Status` — lifecycle status such as `draft`, `accepted`, `deprecated`, `provisional`.

Projects may add columns if needed, but should preserve grep-friendly identifiers.

## Entity lifecycle statuses

Baseline `Status` values:

| Status | Meaning | Agent expectation |
| --- | --- | --- |
| `draft` | Entity is being shaped and is not accepted as stable project knowledge yet. | Do not treat as durable baseline without checking context or owner. |
| `provisional` | Entity is usable for current reasoning, but has explicit assumptions, warnings or unresolved validation needs. | May use with caution; preserve warnings and avoid hiding uncertainty. |
| `accepted` | Entity is accepted as current project SoT for its domain. | May use as baseline and link from relationships/traces/tests/tasks. |
| `deprecated` | Entity was valid before but should no longer be used for new decisions. | Follow replacement note if present; do not create new traces unless migration requires it. |

Projects may add more specific statuses if needed, but these four statuses form the generic traceability baseline.

Status does not replace ownership or rationale. If an Entity instance is `provisional` or `deprecated`, the map row or detail page should explain the reason, replacement, revisit condition or owning workflow when relevant.

## Detail pages

Detail page is useful when:

- Entity instance has substantial behavior or rationale;
- Entity instance participates in many traces;
- Entity instance needs examples, scenarios or constraints;
- Entity instance is important enough that short table row is insufficient.

Detail pages should not replace the map. The map remains the first navigation layer.

## Domain ownership

Each domain owns its own registry.

Examples:

```text
docs/product/entities-map.md
docs/system_design/entities-map.md
docs/architecture/entities-map.md
docs/testing/entities-map.md
```

Generic traceability asset does not prescribe domains. Methodology profiles or project context define concrete domains.

The active project catalog of Entity types, prefixes and registry locations should live in:

```text
docs/traceability/entity-type-catalog.md
```

`project/traceabilityContext.md` should point agents to `docs/traceability/index.md`, not duplicate the full catalog.

## Agent usage

When an agent sees an identifier, preferred navigation is:

```text
project traceability context
  -> docs/traceability/index.md
  -> relevant entities-map.md
  -> Entity row
  -> optional detail page
  -> relationships-map / trace-map for Relationships and Trace chains
```

Grep remains useful as fallback and validation, but should not be the only navigation mechanism.

## Canonical invariants

- Entity maps are Entity instance registries.
- Entity maps are domain-local unless project context chooses another layout.
- Detail pages are optional supporting layer.
- Entity IDs must be stable and searchable.
- Actual project Entity definitions are project-owned SoT.
