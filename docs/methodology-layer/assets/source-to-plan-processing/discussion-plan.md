# Discussion Plan

> Status: Draft  
> Scope: source-to-plan processing  
> Role: current work framing artifact for focused discussion/design

## Назначение

`Discussion Plan` frames current work over selected source ideas.

It answers:

```text
What do we want to discuss or design now, why, and in what order?
```

## Responsibilities

A Discussion Plan should contain:

- goal;
- scope;
- non-goals;
- canonical references;
- selected source anchors;
- decisions already accepted;
- discussion clusters for this plan;
- expected outputs;
- open questions and risks;
- maturity status.

## Cluster meaning

In a Discussion Plan, a cluster is a work-framing unit.

It groups ideas for a specific goal, not for all possible future uses of the source.

One source can support multiple plans with different clusters.

## Loading rule

Agents should load only anchors and docs selected by the current Discussion Plan.

Do not load unrelated source clusters by default.

## Completion rule

When a cluster is materialized, replace active discussion detail with:

```text
decision summary
links to materialized docs
remaining open questions
```

This prevents active plans from becoming historical logs.

## Boundary

Discussion Plan is not a taskset unless explicitly decomposed into executable tasks by project-local task-management rules.
