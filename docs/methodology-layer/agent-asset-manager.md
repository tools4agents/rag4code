# Agent Asset Manager

> Status: Draft  
> Scope: architecture intent для менеджера agent asset packages and project asset environments  
> Role: Source of Truth для разделения package-management и environment-management responsibilities внутри будущего Agent Asset Manager

## Назначение

`Agent Asset Manager` — будущий инструмент HyperGraph для установки, обновления, удаления and materialization agent assets в проектах.

Он вдохновлен `uv`: как `uv` совмещает package management and project environment management для Python, так `Agent Asset Manager` должен быть одной software system, которая совмещает две явно разделенные функции:

1. `package manager` — работает с reusable asset packages and registry.
2. `environment manager` — управляет installed asset environment конкретного проекта.

Разделение функций нужно архитектурно, даже если product/software implementation будет единым CLI/service.

## Responsibility split

```text
Agent Asset Manager
  -> Package Manager responsibilities
  -> Environment Manager responsibilities
```

### Package Manager responsibilities

Package manager side отвечает за reusable package world:

- поиск asset packages в registry или catalog;
- resolution package identity and version;
- dependency and compatibility checks;
- download/copy/install reusable package source;
- update/remove package source;
- проверку package metadata;
- управление relationships вроде `requires`, `recommended_with`, `compatible_with`, `included_in_composition`.

Package manager не владеет project facts.

Он не решает, какие конкретные `US-09`, `ADR-03`, task artifacts или test cases существуют в проекте.

### Environment Manager responsibilities

Environment manager side отвечает за конкретный project asset environment:

- installed asset inventory для проекта;
- materialization templates into project-owned files;
- mapping package assets to project-local paths;
- project-local overrides;
- distinction between package-owned source, generated projection and project-owned SoT;
- drift detection между installed package expectations and project files;
- reconcile installed asset environment после update, removal or manual edits;
- agent-facing context entry points для installed assets.

Environment manager не является package registry and version resolver.

Он применяет уже выбранные packages к конкретному project context.

## Why one tool but two roles

Одна software system полезна потому что user workflow должен быть простым:

```text
agent-assets install adaptive-waterfall
agent-assets sync
agent-assets status
agent-assets update
```

Но внутри эти команды должны сохранять разделение:

```text
install package source
  -> resolve package and dependencies
  -> update project installed asset inventory
  -> materialize or update project-local files
  -> record environment state
```

Без этого разделения tool начнет смешивать reusable package metadata с project-local truth.

## Asset lifecycle

Baseline lifecycle:

```text
discover package
  -> resolve version and compatibility
  -> install package source
  -> register in project asset environment
  -> materialize project-local entry points/templates
  -> use in agent workflow
  -> detect drift or package update
  -> reconcile project environment
```

## Source ownership model

| Layer | Owner | Example |
| --- | --- | --- |
| Package source | asset package / registry | reusable `traceability-system` templates |
| Installed asset inventory | project asset environment | selected assets and versions for one project |
| Project-owned SoT | project | actual `docs/traceability/relationships-map.md`, tasks, docs, code |
| Derived runtime / graph projection | tooling | generated DB projection, MCP query state |

Important invariant:

```text
Agent Asset Manager installs conventions, templates and reusable assets.
Project owns actual project facts.
```

## Relationship to asset taxonomy

Asset types are defined in [`asset-taxonomy-and-composition-model.md`](./asset-taxonomy-and-composition-model.md).

The manager should support installable packages for asset types such as:

- `knowledge-lifecycle asset`;
- `task-management-system asset`;
- `terms-management-system asset`;
- `research-management-system asset`;
- `testing-system asset`;
- `traceability-system asset`;
- `workflow asset`;
- `methodology-workflow asset`;
- `methodology asset`;
- `rules pack`;
- `skills pack`;
- `agent-role pack`;
- `reference pack`.

## Relationship to project context

Project-local context entry points are defined by [`project-context-entry-system`](./assets/project-context-entry-system/index.md).

Agent Asset Manager may materialize or update optional project context files for installed assets, for example:

```text
project/traceabilityContext.md
project/methodologyContext.md
```

Those files are project-owned context artifacts after materialization. Package updates must not overwrite meaningful project-owned edits silently.

## What this document does not define

This document does not define:

- exact CLI syntax;
- package manifest schema;
- registry storage implementation;
- version solver algorithm;
- project installed inventory file format;
- graph ingestion or MCP API contracts.

Those belong to later contracts or implementation specs.

## Canonical invariants

- `Agent Asset Manager` is one future software system with two explicitly separated responsibility areas: package management and environment management.
- Package management owns reusable package resolution and compatibility.
- Environment management owns project-local installed asset state and materialization.
- Package source must not become project fact SoT.
- Project-owned SoT must not be overwritten silently by package updates.
- Derived graph/runtime projections are rebuildable from file-first source layers.
