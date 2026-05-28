# System Design

> Status: Draft  
> Scope: system-level Source of Truth for HyperGraph  
> Role: navigation entry point for system boundary, external behavior and state ownership

## Назначение

Этот раздел фиксирует system-level baseline HyperGraph: какой системой является продукт в своем окружении, какие внешние actors and systems с ним взаимодействуют, где проходят boundaries и кому принадлежит state.

System Design переводит product intent из [`Product Documentation`](../product/index.md) в externally visible behavior and system responsibilities. Internal components and implementation structure фиксируются в Architecture Design.

## Порядок чтения

1. [`project-model.md`](./project-model.md) — system-level модель `project`, root, config, database, isolation and excludes.
2. [`state-ownership.md`](./state-ownership.md) — ownership между Git, filesystem, project files and derived database.
3. [`graph-model.md`](./graph-model.md) — system-level модель graph nodes, classifications, relations and first-iteration boundaries.

## Границы раздела

Этот раздел не фиксирует:
- concrete storage backend;
- internal module decomposition;
- database schema;
- implementation task breakdown;
- final parser or technology choices.
