# Graph Projection

> Status: Draft  
> Scope: derived graph DB and MCP relationship for `traceability-system asset`  
> Role: Source of Truth for graph projection boundaries

## Назначение

Graph projection — derived representation built from markdown/code Source of Truth.

В traceability context graph DB полезна для:

- fast lookup by Entity ID;
- relationship traversal;
- impact analysis;
- MCP-based agent navigation;
- detecting orphan entities or broken relationships.

Но graph DB не является Source of Truth.

## Projection flow

```text
project markdown/code SoT
  -> extract Entity instances, Relationship instances, Trace chain instances and code/test metadata
  -> build graph DB projection
  -> expose query interface via MCP or tools
```

## Semantic-to-graph mapping

Traceability SoT uses Entity / Relationship / Trace chain terminology by default. Graph terms are technical projection terms:

```text
Entity instance -> graph vertex
Relationship instance -> graph edge
Trace chain instance -> curated graph path over Relationship instances
```

This mapping is one-way for ownership: graph projection may accelerate traversal, but source files own active traceability facts.

## MCP role

MCP can answer questions like:

```text
What is US-09?
What entities are connected to COMP-07?
Which tests verify this requirement?
Which ADRs constrain this component?
```

MCP answer should be backed by source references. If graph projection conflicts with markdown/code SoT, SoT wins.

## Drift and rebuild

Projection drift happens when graph DB state no longer matches source files.

Examples:

- Entity instance removed from `entities-map.md` but still exists in graph DB;
- Relationship instance changed in `relationships-map.md` but old graph edge remains;
- code/test metadata changed but projection not rebuilt.

The projection must be rebuildable from source layers.

## What projection does not own

Graph projection does not own:

- product decisions;
- architecture decisions;
- system design records;
- test design truth;
- task status;
- release notes;
- identifier assignment.

It only represents and accelerates navigation across source facts.

## Canonical invariants

- Graph DB is derived projection.
- MCP is a query/navigation interface over projection.
- Markdown/code SoT wins over projection conflicts.
- Projection must be rebuildable.
- Projection should preserve source references for explainability.
