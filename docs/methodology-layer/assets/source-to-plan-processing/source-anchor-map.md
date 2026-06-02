# Source Anchor Map

> Status: Draft  
> Scope: source-to-plan processing  
> Role: traceability artifact for large source inputs

## Назначение

`Source Anchor Map` is a compact navigation artifact for a large source.

It answers:

```text
What exists in this source and where can it be reread?
```

## Responsibilities

A Source Anchor Map should capture:

- source identity and provenance;
- source scope;
- line ranges, sections or other anchors;
- compact topic map;
- idea inventory summary;
- already materialized decisions/docs;
- canonical warnings;
- source-specific terminology traps;
- references to related discussion plans.

## What it is not

Source Anchor Map is not:

- current work plan;
- taskset;
- accepted architecture document;
- full summary of every source paragraph;
- replacement for reading relevant source anchors.

## Materialized decisions

When ideas from the source become project docs, contracts or term pages, update the map:

```text
idea -> materialized in <doc/term/contract>
```

This prevents agents from reopening completed discussion clusters.

## Canonical warnings

Warnings are compact rules that prevent known regressions.

Examples:

```text
Do not use outdated term X.
Do not treat raw discussion Y as accepted architecture.
Use materialized doc Z instead of source discussion lines.
```

## Boundary

The map preserves traceability to a source. It does not decide current work priority. Current priority belongs to a Discussion Plan.
