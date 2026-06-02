# Input Layer

> Status: Draft  
> Scope: source-to-plan processing  
> Role: boundary for raw source inputs

## Назначение

`Input Layer` contains raw source material selected for processing.

It is the entry point for extraction, anchoring, idea inventory and later discussion planning.

## Input examples

Input can include:

- LLM chat discussion history;
- raw architecture or product discussion;
- documentation fragment;
- scientific paper;
- article or book chapter;
- research note;
- ADR draft;
- codebase exploration transcript;
- meeting notes.

## Core rule

Input is not Source of Truth.

```text
Input = raw material for processing.
Source of Truth = accepted project layer after review/materialization.
```

Raw input may contain contradictions, outdated names, exploratory hypotheses and wrong assumptions.

## Processing goal

The goal is not to copy input into project docs.

The goal is to extract useful ideas with traceability:

```text
raw source
  -> source anchors
  -> idea inventory
  -> focused plan
  -> materialized project artifacts
```

## Handling rules

- Preserve original source when possible.
- Do not rewrite source as accepted knowledge.
- Do not treat raw discussion conclusions as decisions until materialized.
- Keep source provenance visible.
- Use source anchors for later rereading instead of dumping long excerpts into active plans.

## Boundary

Input Layer owns raw source storage and provenance.

It does not own accepted terminology, architecture decisions, contracts or executable tasks.
