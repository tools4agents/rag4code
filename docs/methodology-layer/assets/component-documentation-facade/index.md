# Component Documentation Facade

> Status: Draft  
> Scope: methodology-layer assets  
> Role: навигация по practice создания component-facing документации для быстрого operational onboarding без source-first discovery

## Назначение

Этот asset фиксирует practice создания `Component Documentation Facade` для component sources.

`Component Documentation Facade` — первый orientation layer для человека или агента, которому нужно понять и использовать component без чтения исходного кода как default discovery path.

Фасад не заменяет source code, design docs или ADR. Он помогает сначала понять:

```text
что это за component
когда его использовать
как его запустить
какие contracts/config/env важны
как он используется соседними runtime/runner/orchestrator слоями
куда идти дальше
```

## Core formula

```text
README.md
  -> docs/operational-guide.md for quick operational use
    -> focused operational docs for the current question
  -> docs/index.md when full documentation map is needed
    -> design / ADR / rationale / source code when task requires deeper context
```

## Когда использовать

Используй этот pattern, если:

- создан новый component source;
- component exposes CLI, HTTP service, package API, adapter contract or integration route;
- component будет использоваться другими developers, agents, contributors or integration tests;
- source-first discovery может перегрузить context window;
- нужно отделить quick operational usage от design/ADR/motivation documentation.

## Files

- [`SKILL.md`](./SKILL.md) — короткая operational instruction для агента.
- [`rationale.md`](./rationale.md) — explanation of why facade-first documentation scales better than source-first discovery.
- [`structure.md`](./structure.md) — practical layout guide for README, `operational-guide.md`, focused docs and optional `docs/index.md`.

## Facade vs full documentation map

`docs/operational-guide.md` отвечает:

```text
How do I quickly understand and use this component safely?
```

`docs/index.md` отвечает:

```text
What documentation exists for this component, and where are the entry points / Source of Truth for each topic?
```

Small components may start without `docs/index.md`. Create `docs/index.md` when component docs grow beyond the operational facade: ADRs, design notes, rationale, multiple contracts, evidence or test documentation.

## Source code boundary

The facade is the first orientation layer, not a source-code ban.

Read source code when the task requires:

- changing behavior;
- debugging implementation issues;
- resolving ambiguity in facade docs;
- investigating undocumented edge cases;
- verifying implementation details.

## Boundary

This asset does not define a universal project layout for all repositories. It defines a reusable documentation practice for component sources.

It also does not replace [`batched-artifact-generation`](../batched-artifact-generation/index.md). Use that asset when creating or updating the facade requires multiple related documentation artifacts.
