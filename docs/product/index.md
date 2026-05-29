# Product Documentation

> Status: Draft  
> Scope: product-level Source of Truth for HyperGraph  
> Role: navigation entry point for product intent, scope and capabilities

## Назначение

Этот раздел фиксирует product-level baseline HyperGraph: зачем создается продукт, для кого он предназначен, какие capabilities он должен дать и что входит в первую итерацию.

Product documentation отвечает на вопрос: какой продукт мы делаем и за что он должен отвечать. System boundary и internal architecture фиксируются в отдельных design layers.

## Порядок чтения

1. [`vision.md`](./vision.md) — product intent, actors, value and long-term direction.
2. [`first-iteration-scope.md`](./first-iteration-scope.md) — scope первой итерации, MVP capabilities and non-goals.
3. [`future-capabilities.md`](./future-capabilities.md) — future capability directions outside first iteration scope.

Related system-level product note:
- [`project-config-format.md`](../system_design/project-config-format.md) — TOML decision for project-local shared config.

## Границы раздела

Этот раздел не фиксирует:
- detailed system boundary;
- storage backend choice;
- internal component architecture;
- implementation task breakdown.
