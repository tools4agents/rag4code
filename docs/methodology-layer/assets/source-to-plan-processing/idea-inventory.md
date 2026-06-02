# Idea Inventory

> Status: Draft  
> Scope: source-to-plan processing  
> Role: semantic extraction artifact for candidate ideas

## Назначение

`Idea Inventory` captures candidate ideas extracted from one or more sources.

It focuses on meaning, not just navigation.

## Responsibilities

Idea Inventory may contain:

- raw idea clusters;
- candidate project uses;
- dependencies between ideas;
- related accepted terms;
- materialized ideas;
- rejected or superseded ideas;
- unknowns and risks.

## Status model

Recommended idea statuses:

```text
raw
candidate
active-in-plan
materialized
rejected
superseded
parked
```

## Relation to Source Anchor Map

Source Anchor Map preserves where ideas came from.

Idea Inventory records what ideas mean and how they relate.

For small sources, Idea Inventory can be a section inside Source Anchor Map. For large sources, keep it separate.

## Relation to Discussion Plan

Discussion Plan selects a subset of ideas for current work.

It should not pull every parked idea into active context.

## Boundary

Idea Inventory is not Source of Truth. Materialization into project docs, terms, contracts or tasks is required before ideas become accepted project baseline.
