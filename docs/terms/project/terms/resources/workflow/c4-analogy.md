# Workflow and C4 Analogy

> Status: Draft  
> Scope: adjacent resource for [`workflow`](../../workflow.md)  
> Role: explanatory analogy for progressive disclosure across workflow levels

## Назначение

Этот документ объясняет nested workflow через аналогию с C4-style progressive disclosure.

Аналогия нужна, чтобы отделять обзор процесса, внутренние stage workflows, bounded steps и concrete execution capabilities.

## Core analogy

C4 diagrams раскрывают систему слоями. Workflow documentation может раскрывать процесс похожим образом.

```text
C4 Level 1: System Context
C4 Level 2: Container
C4 Level 3: Component
C4 Level 4: Code
```

Workflow-level analogy:

```text
Workflow Level 1: top-level methodology workflow
Workflow Level 2: stage workflow / nested workflow
Workflow Level 3: workflow-step
Workflow Level 4: skill, command projection or concrete agent action
```

## Example

```text
Software Development Methodology (workflow)
  -> Discovery & Intent Framing (nested workflow / stage workflow)
      -> Intake and context classification (workflow-step)
      -> Workspace activation (workflow-step)
      -> Research subworkflow (nested workflow)
          -> Research task setting (workflow-step)
          -> Research execution (workflow-step)
          -> Research synthesis (workflow-step)
```

The top-level workflow should not inline all internals of `Research subworkflow`.

It should link to its nested workflow overview and state only parent-level transition expectations.

## Why this analogy helps documentation

The analogy supports progressive disclosure:

- parent workflow remains compact;
- nested workflow owns its internal graph;
- `workflow-step` owns bounded execution semantics;
- support resources and skills stay below step/process maps.

This prevents a single markdown file from becoming a monolithic instruction document.

## Practical rule

Use the lowest level that carries the correct meaning:

- high-level navigation and stage order belongs in parent `workflow.md`;
- internal stage process belongs in nested `workflow.md`;
- bounded executable unit belongs in `STEP.md`;
- reusable capability belongs in skill or runtime-specific projection.

## Boundary of the analogy

This analogy does not require workflow docs to copy C4 notation.

It only says that workflow documentation should support layered disclosure in the same spirit: from broad context to detailed execution units.
