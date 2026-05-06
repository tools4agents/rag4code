# Edge and Trace Maps

> Status: Draft  
> Scope: edge map and trace map conventions inside `traceability-system asset`  
> Role: Source of Truth для markdown representation of graph edges and meaningful traces

## Назначение

Этот документ разделяет два слоя traceability:

```text
edges-map.md = atomic graph edges
trace-map.md = curated meaningful paths over edges
```

Оба слоя являются markdown Source of Truth for graph-ready relationships.

## Edges map

Edges map stores atomic relationships between entity IDs.

Recommended location:

```text
docs/traceability/edges-map.md
```

Recommended table:

```markdown
| From | Relationship | To | Source | Status | Notes |
| --- | --- | --- | --- | --- | --- |
| ENT-A | relates-to | ENT-B | `docs/example/entities-map.md` | accepted | Short rationale. |
```

Column meaning:

- `From` — source entity ID;
- `Relationship` — edge label;
- `To` — target entity ID;
- `Source` — document or evidence source for the relationship;
- `Status` — `draft`, `accepted`, `provisional`, `deprecated` or project-selected status;
- `Notes` — short rationale or qualification.

## Trace map

Trace map stores meaningful paths that humans and agents need often.

Recommended location:

```text
docs/traceability/trace-map.md
```

Recommended table:

```markdown
| Trace ID | Chain | Meaning | Status | Notes |
| --- | --- | --- | --- | --- |
| TR-001 | `ENT-A -> ENT-B -> ENT-C` | Why this path matters. | accepted | Optional note. |
```

Trace chain is not a replacement for edges. It is a curated path over atomic edges.

## Why both maps exist

Atomic edges are good for graph projection and precise relationship maintenance.

Trace chains are good for agent and human reasoning:

```text
failed test
  -> test case
  -> behavior
  -> requirement
  -> architecture decision
  -> component
```

Without trace chains, agents may need to reconstruct common paths repeatedly.

Without atomic edges, trace chains become hard to validate and project into graph DB.

## Relationship labels

Generic traceability asset does not freeze a global relationship catalog.

Methodology profiles may recommend labels, but the active project label catalog should live in:

```text
docs/traceability/relationship-label-catalog.md
```

Projects should define common labels there, for example:

- `details`;
- `realizes`;
- `supports`;
- `constrains`;
- `verifies`;
- `implemented-by`;
- `depends-on`.

## Canonical invariants

- Edges map contains atomic relationships.
- Trace map contains curated meaningful paths.
- Trace chains should be explainable from edges.
- Relationship facts are project-owned markdown SoT.
- Graph DB edges must be derivable from markdown/code source layers.
