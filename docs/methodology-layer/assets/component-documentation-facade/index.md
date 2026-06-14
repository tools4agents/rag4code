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
  -> docs/operational_index.md for quick operational onboarding
       -> docs/operational-guide.md
       -> focused operational docs for the current question

  -> docs/index.md for full stable component documentation map
       -> contracts / design / ADR / rationale / test docs as needed

  -> docs/develop_index.md for development-only context, when it exists
       -> docs/develop/active_focus.md
       -> docs/develop/discussions/open_questions.md
```

## Когда использовать

Используй этот pattern, если:

- создан новый component source;
- component exposes CLI, HTTP service, package API, adapter contract or integration route;
- component будет использоваться другими developers, agents, contributors or integration tests;
- source-first discovery может перегрузить context window;
- нужно отделить quick operational usage от design/ADR/motivation documentation.

Для component source, который еще является заготовкой и не имеет стабильного operational surface, не создавай искусственный operational facade. Начни с pre-facade development route:

```text
README.md
docs/develop_index.md
docs/develop/active_focus.md
```

Такой нулевой шаг фиксирует роль заготовки, current development focus и ссылки на project-level Source of Truth, не выдавая незрелый component за готовый к operational usage.

## Files

- [`SKILL.md`](./SKILL.md) — короткая operational instruction для агента.
- [`entry-points.md`](./entry-points.md) — intent-based модель трех entry points: operational, stable map и development-only route.
- [`rationale.md`](./rationale.md) — explanation of why facade-first documentation scales better than source-first discovery.
- [`structure.md`](./structure.md) — practical layout guide for README, `operational-guide.md`, focused docs and optional `docs/index.md`.

## Entry points

The facade uses intent-based routing:

```text
docs/operational_index.md
  answers: how do I quickly understand and use this component?

docs/index.md
  answers: what stable documentation exists for this component?

docs/develop_index.md
  answers: how do I continue development and find current state/history?
```

Detailed rules are defined in [`entry-points.md`](./entry-points.md).

## Facade vs full documentation map

`docs/operational_index.md` and `docs/operational-guide.md` отвечают:

```text
How do I quickly understand and use this component safely?
```

`docs/index.md` отвечает:

```text
What documentation exists for this component, and where are the entry points / Source of Truth for each topic?
```

Small components may start without `docs/index.md`. Create `docs/index.md` when component docs grow beyond the operational facade: ADRs, design notes, rationale, multiple contracts, evidence or test documentation.

Create `docs/develop_index.md` only when development-only artifacts exist. Development-only artifacts should live under `docs/develop/` and must not be directly linked from the operational facade.

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
