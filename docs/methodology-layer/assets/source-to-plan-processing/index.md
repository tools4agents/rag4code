# Source-to-Plan Processing

> Status: Draft  
> Scope: methodology-layer assets  
> Role: навигация по pattern обработки больших source inputs into focused plans

## Назначение

Эта папка описывает pattern для обработки больших входных источников: discussions, documents, papers, research notes and other raw inputs.

Pattern помогает агенту не превращать raw source в active task noise, а отделять source navigation, idea extraction, planning and materialization.

## Core formula

```text
Input Source
  -> Source Anchor Map / Idea Inventory
    -> Discussion Plan
      -> Focused Materialization
        -> Feedback Loop
```

Коротко:

```text
Input is raw material.
Source Anchor Map preserves traceability.
Idea Inventory extracts candidate meaning.
Discussion Plan frames current work.
Materialization creates project docs/contracts/tasks.
```

## Reading order

1. [`source-to-plan-processing-pattern.md`](./source-to-plan-processing-pattern.md) — overview and core pattern.
2. [`input-layer.md`](./input-layer.md) — what belongs to input layer and why input is not Source of Truth.
3. [`source-anchor-map.md`](./source-anchor-map.md) — source traceability and anchor map artifact.
4. [`idea-inventory.md`](./idea-inventory.md) — extracted ideas and materialization status.
5. [`discussion-plan.md`](./discussion-plan.md) — current work framing and cluster decomposition.
6. [`materialization-and-feedback-loop.md`](./materialization-and-feedback-loop.md) — how completed work feeds back into maps and plans.

## Templates

- [`source-anchor-map-template.md`](./templates/source-anchor-map-template.md)
- [`idea-inventory-template.md`](./templates/idea-inventory-template.md)
- [`discussion-plan-template.md`](./templates/discussion-plan-template.md)

## Boundary

This pattern does not replace project-specific task management, research management or terms management.

It provides a processing layer between raw inputs and project-specific materialization artifacts.
