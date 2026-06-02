# Materialization and Feedback Loop

> Status: Draft  
> Scope: source-to-plan processing  
> Role: lifecycle rules after discussion or design work is completed

## Назначение

This document describes how source-to-plan work feeds back into maps, plans and project artifacts.

The goal is to preserve decisions without keeping full discussion history as active context noise.

## Materialization outputs

Materialization may create or update:

- focused architecture docs;
- term pages;
- contract drafts;
- plan artifacts;
- task artifacts;
- ADRs;
- product docs;
- source anchor maps.

## Feedback loop

After materialization:

```text
1. Update Source Anchor Map with materialized docs.
2. Mark idea status as materialized / superseded / parked.
3. Remove completed cluster detail from active plan.
4. Keep compact decision summary.
5. Create a new plan for remaining work if needed.
```

## What to avoid

Do not leave completed work as active planning noise.

Avoid:

- full chat history in handoff;
- full file update log in plan;
- completed clusters mixed with next work;
- raw source discussion treated as accepted architecture after materialization.

## Decision summary

Decision summary should be compact and action-oriented.

It should include:

- accepted decisions;
- links to materialized docs;
- do-not-reopen notes;
- remaining open questions.

## Boundary

Feedback loop maintains knowledge hygiene. It does not replace project-specific review, approval or Source of Truth promotion rules.
