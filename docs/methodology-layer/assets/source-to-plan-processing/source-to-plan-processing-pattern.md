# Source-to-Plan Processing Pattern

> Status: Draft  
> Scope: methodology-layer assets  
> Role: overview of source-to-plan processing pattern

## Назначение

`Source-to-Plan Processing` is a pattern for turning large raw sources into focused project work without losing traceability.

It is useful when a source contains many potentially valuable ideas, but only part of them is relevant to the current task.

## Pattern

```text
Input Source
  -> Source Anchor Map / Idea Inventory
    -> Discussion Plan
      -> Focused Materialization
        -> Updated Source Anchor Map / Next Plan
```

## Core distinction

`Source Anchor Map` answers:

```text
What exists in the source and where can it be reread?
```

`Discussion Plan` answers:

```text
What do we want to discuss or design now, why, and in what order?
```

These are different artifacts. The first preserves source traceability. The second frames current work.

## Analogy

The pattern is similar to:

- literature review;
- Zettelkasten-style knowledge extraction;
- deep wiki source navigation;
- thesis work with citations and focused chapters.

## Agent benefit

This pattern helps agents:

- avoid rereading huge raw sources by default;
- load only source anchors relevant to the current plan;
- avoid reopening already materialized decisions;
- maintain multiple focused plans over one large source;
- remove completed discussion clusters from active context noise.

## Output types

Typical outputs:

```text
source-anchor-map.md
idea-inventory.md
discussion-plan.md
focused docs / term pages / contracts / task artifacts
```

## Boundary

The pattern does not decide what is accepted project knowledge. Acceptance belongs to project-specific Source of Truth rules.
