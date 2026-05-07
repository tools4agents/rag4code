# Traceability System Asset

> Status: Draft  
> Scope: generic traceability model для project Entity instances, Relationship instances and Trace chain instances  
> Role: Source of Truth для mechanics reusable `traceability-system asset`

## Назначение

`traceability-system asset` — reusable asset type, который задает markdown-first модель traceability.

Короткая формула:

```text
Entity registries define Entity instances
relationships-map defines Relationship instances
trace-map defines meaningful Trace chain instances
graph database is derived projection
```

Graph terminology is derived-projection terminology, not canonical traceability Source of Truth wording:

```text
Entity instance -> graph vertex
Relationship instance -> graph edge
Trace chain instance -> curated graph path
```

## Core concepts

### Entity registry

Entity registry — карта Entity instances, которые должны стать agent-readable navigation anchors and can be projected as graph vertices.

Обычно materialize-ится как:

```text
docs/<domain>/entities-map.md
docs/<domain>/entities/<entity-id>.md
```

### Relationship registry

Relationship registry — markdown registry of Relationship instances между Entity instances.

Canonical semantic filename:

```text
docs/traceability/relationships-map.md
```

### Trace map

Trace map — curated collection of meaningful Trace chain instances over Relationships.

Обычно materialize-ится как:

```text
docs/traceability/trace-map.md
```

### Entity type catalog

Entity type catalog defines active project Entity types, Entity Identifier families/patterns, domains and registries.

Recommended location:

```text
docs/traceability/entity-type-catalog.md
```

This catalog is project-level SoT for questions like:

```text
What does US-* mean in this project?
Where should an agent look up SYSDR-* entities?
Which prefixes are active, provisional or deprecated?
```

### Relationship type catalog

Relationship type catalog defines allowed or recommended Relationship types and their semantics.

Recommended location:

```text
docs/traceability/relationship-type-catalog.md
```

This catalog prevents `relationships-map.md` from using ambiguous Relationship type values without shared meaning. If a stored table cell is called a label in implementation context, that label is only the stored representation of a Relationship type value.

### Project traceability context

Project traceability context tells agents where traceability entry points live in this project.

Recommended location:

```text
project/traceabilityContext.md
```

This file should stay thin. It points to `docs/traceability/index.md`, while detailed catalogs live in `docs/traceability/`.

## Layered ownership model

| Layer | Typical location | Responsibility |
| --- | --- | --- |
| Generic traceability asset | `docs/methodology-layer/assets/traceability/` | Defines mechanics: Entity registries, Relationship registries, Trace maps, catalogs and graph projection rule. |
| Methodology traceability profile | methodology-specific resources | Defines which domains, Entity families and Trace chains matter for a methodology. |
| Project traceability context | `project/traceabilityContext.md` | Thin project routing entry point to the active traceability docs. |
| Project traceability catalogs | `docs/traceability/entity-type-catalog.md`, `relationship-type-catalog.md` | Active project SoT for Entity types, identifier patterns and Relationship type meanings. |
| Project traceability instance | `docs/traceability/*`, `docs/<domain>/entities-map.md` | Actual project Entity instances, Relationship instances and Trace chain instances. |
| Derived graph projection | graph DB / MCP runtime | Rebuildable query/navigation projection over source facts. |

## Source of Truth rule

Traceability facts are authored in markdown/code SoT.

Graph DB and MCP are derived projection and query layer:

```text
markdown/code SoT
  -> graph extraction / ingestion
  -> graph DB projection
  -> MCP query/navigation
```

The graph DB must be rebuildable from source layers.

## Generic vs methodology-specific ownership

This asset owns generic mechanics:

- registry shape;
- Relationship and Trace chain concepts;
- identifier requirements;
- project entrypoint pattern;
- derived graph projection rule.

Methodology-specific profile owns concrete traceability expectations. For example, an SDLC methodology may say that product entities should connect to system design entities, architecture entities and tests.

Project owns actual facts: concrete Entity IDs, Relationship instances and Trace chain instances.

## Identifier requirements

Entity identifiers should be:

- stable;
- unique within their identifier family or domain;
- grep-friendly;
- regex-friendly;
- short enough for human reference;
- explicit enough to avoid collision with generic prose.

This asset does not freeze global identifier grammar. Methodology profiles and projects may define specific prefixes.

## Canonical invariants

- Entity registries define Entity instances.
- Relationship registries define atomic Relationship instances.
- Trace maps define curated meaningful paths over Relationship instances.
- Markdown/code remains Source of Truth.
- Graph DB and MCP state are derived and rebuildable.
- Generic traceability mechanics must not be coupled to one methodology.
- Project facts must not be hidden only in graph DB.
