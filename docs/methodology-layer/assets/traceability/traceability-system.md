# Traceability System Asset

> Status: Draft  
> Scope: generic traceability model для project graph vertices, edges and traces  
> Role: Source of Truth для mechanics reusable `traceability-system asset`

## Назначение

`traceability-system asset` — reusable asset type, который задает markdown-first модель traceability.

Короткая формула:

```text
entity registries define vertices
edges-map defines atomic edges
trace-map defines meaningful paths
graph database is derived projection
```

## Core concepts

### Entity registry

Entity registry — карта сущностей, которые должны стать graph vertices или agent-readable navigation anchors.

Обычно materialize-ится как:

```text
docs/<domain>/entities-map.md
docs/<domain>/entities/<entity-id>.md
```

### Edge map

Edge map — markdown registry atomic relationships между entities.

Обычно materialize-ится как:

```text
docs/traceability/edges-map.md
```

### Trace map

Trace map — curated collection of meaningful paths over edges.

Обычно materialize-ится как:

```text
docs/traceability/trace-map.md
```

### Project traceability context

Project traceability context tells agents where traceability entry points live in this project.

Recommended location:

```text
project/traceabilityContext.md
```

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
- edge and trace concepts;
- identifier requirements;
- project entrypoint pattern;
- derived graph projection rule.

Methodology-specific profile owns concrete traceability expectations. For example, an SDLC methodology may say that product entities should connect to system design entities, architecture entities and tests.

Project owns actual facts: concrete entity IDs, edges and traces.

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

- Entity registries define graph vertices.
- Edge maps define atomic graph relationships.
- Trace maps define curated meaningful paths over edges.
- Markdown/code remains Source of Truth.
- Graph DB and MCP state are derived and rebuildable.
- Generic traceability mechanics must not be coupled to one methodology.
- Project facts must not be hidden only in graph DB.
