# Project Context Entry System

## Назначение

Этот документ фиксирует concrete reusable implementation [`project-context-entry-system asset`](../../../terms/project/terms/project-context-entry-system-asset.md).

Он отвечает на вопросы:

- какие файлы составляют baseline package project context entry layer;
- какие из них обязательны, а какие optional;
- как между ними распределяется ownership;
- какие templates нужно использовать при bootstrap нового проекта.

## Что задает asset

`Project-context-entry-system` задает:

- root-level router artifact `AGENTS.md`;
- `project/` как durable context layer;
- baseline file set внутри `project/`;
- reusable templates для project initialization.

## Canonical invariants

- `AGENTS.md` должен оставаться thin router artifact.
- Durable project context должен жить в `project/`, а не в `AGENTS.md`.
- `project/index.md` владеет составом durable project context layer и кратким boundary summary.
- `project/entry-points.md` владеет routing/loading contract и ownership split между context layers.
- `project/index.md` не должен дублировать routing contract из `project/entry-points.md`.
- `project/` не должен подменять `docs/` как engineering SoT.
- `project/` не должен подменять `operational_scope/` как execution layer.
- Secret handling baseline должен иметь отдельный explicit file.
- Optional files materialize-ятся только при реальной необходимости.

## Baseline file set

### Root

- `AGENTS.md`

### Mandatory `project/` files

- `index.md`
- `overview.md`
- `gitContext.md`
- `techContext.md`
- `secretsContext.md`
- `entry-points.md`

### Optional `project/` files

- `codeStyle.md`
- `repository-map.md`
- `context-migration.md`

## Template package

Templates живут в [`resources/`](./resources/).

Они дают reusable starting point, но не заменяют project-specific adaptation.

## What this document does not do

Этот документ не задает:

- engineering architecture;
- task storage model;
- glossary system;
- Kilo-specific runtime config internals.
