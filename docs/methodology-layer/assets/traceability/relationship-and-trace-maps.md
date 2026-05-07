# Relationship and Trace Maps

> Status: Draft  
> Scope: Relationship registry and Trace map conventions inside `traceability-system asset`  
> Role: Source of Truth для markdown representation of Relationship instances and meaningful Trace chain instances

## Назначение

Этот документ разделяет два слоя traceability:

```text
relationships-map.md = atomic Relationship instances
trace-map.md = curated meaningful paths over Relationships
```

Оба слоя являются markdown Source of Truth for graph-ready traceability. Technical graph edges are derived from Relationship instances and are not the semantic Source of Truth terminology.

## Relationship registry

Relationship registry stores atomic Relationship instances between Entity instance IDs.

Canonical semantic filename:

```text
docs/traceability/relationships-map.md
```

Recommended table:

```markdown
| From | Relationship type | To | Source | Status | Notes |
| --- | --- | --- | --- | --- | --- |
| ENT-A | relates-to | ENT-B | `docs/example/entities-map.md` | accepted | Short rationale. |
```

Column meaning:

- `From` — source Entity instance ID;
- `Relationship type` — semantic type of Relationship, preferably from `relationship-type-catalog.md`;
- `To` — target Entity instance ID;
- `Source` — document or evidence source for the Relationship;
- `Status` — `draft`, `accepted`, `provisional`, `deprecated` or project-selected status;
- `Notes` — short rationale or qualification.

If an implementation or table parser calls the stored type value a `label`, treat that as storage representation only. The semantic concept remains Relationship type.

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

Trace chain is not a replacement for Relationship instances. It is a curated path over atomic Relationships.

## Why both registries exist

Atomic Relationship instances are good for graph projection and precise relationship maintenance.

Trace chains are good for agent and human reasoning:

```text
failed test
  -> test case
  -> behavior
  -> requirement
  -> architecture decision
  -> component
```

Without Trace chains, agents may need to reconstruct common paths repeatedly.

Without atomic Relationship instances, Trace chains become hard to validate and project into graph DB.

## Relationship types

Generic traceability asset does not freeze a global Relationship type catalog.

Methodology profiles may recommend Relationship types, but the active project Relationship type catalog should live in:

```text
docs/traceability/relationship-type-catalog.md
```

Projects should define common Relationship types there, for example:

- `details`;
- `realizes`;
- `supports`;
- `constrains`;
- `verifies`;
- `implemented-by`;
- `depends-on`.

## Canonical invariants

- Relationship registry contains atomic Relationship instances.
- Trace map contains curated meaningful paths.
- Trace chains should be explainable from Relationship instances.
- Relationship facts are project-owned markdown SoT.
- Graph DB edges must be derivable from markdown/code source layers.
