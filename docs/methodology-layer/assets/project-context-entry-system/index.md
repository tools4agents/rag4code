# Project Context Entry System

> Status: Draft  
> Scope: concrete [`project-context-entry-system asset`](../../../terms/project/terms/project-context-entry-system-asset.md)  
> Role: Source of Truth для reusable package project context entry files и templates

## Назначение

Этот пакет фиксирует concrete [`project-context-entry-system asset`](../../../terms/project/terms/project-context-entry-system-asset.md) для инициализации новых проектов.

Он нужен, чтобы:

- materialize-ить тонкий `AGENTS.md` как router artifact;
- materialize-ить `project/` как durable context layer;
- согласованно разделять `project/`, `docs/`, `operational_scope/` и target-specific runtime layers;
- переиспользовать templates между проектами.

## Что входит в asset package

- [`project-context-entry-system.md`](./project-context-entry-system.md) — каноническая модель concrete asset-а.
- [`agents-md.md`](./agents-md.md) — роль и границы `AGENTS.md`.
- [`project-layer.md`](./project-layer.md) — роль `project/` как durable context layer.
- [`project-entry-points.md`](./project-entry-points.md) — назначение `project/entry-points.md` как routing/loading contract, не индекса состава `project/`.
- [`git-context.md`](./git-context.md) — роль `project/gitContext.md`.
- [`tech-context.md`](./tech-context.md) — роль `project/techContext.md`.
- [`secrets-context.md`](./secrets-context.md) — роль `project/secretsContext.md`.
- [`code-style.md`](./code-style.md) — optional role `project/codeStyle.md`.
- [`repository-map.md`](./repository-map.md) — optional role `project/repository-map.md`.
- [`context-migration.md`](./context-migration.md) — optional role `project/context-migration.md`.
- [`resources/`](./resources/) — reusable templates.

## Baseline layout

```text
AGENTS.md
project/
  index.md
  overview.md
  gitContext.md
  techContext.md
  secretsContext.md
  entry-points.md
  codeStyle.md                # optional
  repository-map.md           # optional
  context-migration.md        # optional
```

## Mandatory vs optional files

### Mandatory baseline

- `AGENTS.md`
- `project/index.md`
- `project/overview.md`
- `project/gitContext.md`
- `project/techContext.md`
- `project/secretsContext.md`
- `project/entry-points.md`

### Optional files

- `project/codeStyle.md`
- `project/repository-map.md`
- `project/context-migration.md`

Optional files materialize-ятся только если они реально полезны для проекта.

## Template package

Baseline templates:

- [`AGENTS.template.md`](./resources/AGENTS.template.md)
- [`project-index.template.md`](./resources/project-index.template.md)
- [`project-overview.template.md`](./resources/project-overview.template.md)
- [`project-git-context.template.md`](./resources/project-git-context.template.md)
- [`project-tech-context.template.md`](./resources/project-tech-context.template.md)
- [`project-secrets-context.template.md`](./resources/project-secrets-context.template.md)
- [`project-entry-points.template.md`](./resources/project-entry-points.template.md)
- [`project-code-style.template.md`](./resources/project-code-style.template.md)
- [`project-repository-map.template.md`](./resources/project-repository-map.template.md)
- [`project-context-migration.template.md`](./resources/project-context-migration.template.md)

## Связь с focused spec

Этот asset package нужно читать вместе с [`repository-context-entry-model.md`](../../repository-context-entry-model.md).

Разделение ответственности такое:

- focused spec задает semantic model entry points;
- этот asset package задает reusable implementation package и templates.

## Связь с другими asset systems

- `project-context-entry-system` не заменяет `knowledge-lifecycle asset`.
- Он не заменяет `task-management-system asset`.
- Он не заменяет `terms-management-system asset`.

Он отвечает только за project context entry layer.
