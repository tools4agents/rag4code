# Asset Environment Project Manager

> Status: Draft  
> Scope: project-local responsibility area внутри будущего Agent Asset Manager  
> Role: Source of Truth для installed asset environment, project-local materialization and reconcile responsibilities

## Назначение

`Asset Environment Project Manager` — responsibility area будущего [`Agent Asset Manager`](./agent-asset-manager.md), которая управляет установленными agent assets внутри конкретного проекта.

Если package manager side отвечает за reusable packages, то environment manager side отвечает за вопрос:

```text
Какие agent assets установлены в этом project, где они materialized,
какие project-owned files они создали, и согласовано ли installed environment состояние?
```

Это не отдельный обязательный software product. Это архитектурно выделенная функция внутри единого Agent Asset Manager.

## Boundary

### This responsibility area does

- хранит или обслуживает installed asset inventory проекта;
- знает, какие package assets активны в проекте;
- materialize-ит templates and entry points into project-local files;
- tracks package-owned source vs project-owned materialized files;
- поддерживает project-local overrides;
- проверяет drift между expected materialization and actual files;
- выполняет reconcile после package update, removal or manual edits;
- помогает агенту найти installed asset entry points.

### This responsibility area does not

- не является global package registry;
- не владеет reusable package source;
- не решает version compatibility самостоятельно без package manager side;
- не принимает product, architecture, system or testing decisions;
- не превращает generated projection в Source of Truth;
- не удаляет project-owned content без explicit policy or human approval.

## Installed asset inventory

Project asset environment needs an inventory of installed assets.

The exact file format is not defined yet, but semantically inventory should answer:

- which assets are installed;
- which versions or version refs are selected;
- which assets are direct vs transitive dependencies;
- where each asset is materialized;
- which project-local files are owned, generated, templated or manually maintained;
- which compatibility profile or composition selected them.

Possible future file examples:

```text
project/agent-assets.md
project/agent-assets.lock.yaml
.hypergraph/asset-environment.json
```

The exact location and format remain open.

## Materialization model

Environment manager materializes reusable packages into project-local context and docs.

Example for traceability:

```text
traceability-system package templates
  -> project/traceabilityContext.md
  -> docs/traceability/index.md
  -> docs/traceability/edges-map.md
  -> docs/traceability/trace-map.md
```

Example for SDLC methodology profile:

```text
adaptive-waterfall methodology package
  -> selected workflow docs / references
  -> project-local methodology context
  -> optional stage-specific templates
```

After materialization, actual project facts inside generated files may become project-owned SoT depending on file role.

## File ownership classes

Environment manager should distinguish file ownership classes.

| Class | Meaning | Update behavior |
| --- | --- | --- |
| `package-source` | reusable source file managed by package registry/cache | updated by package update |
| `generated-projection` | rebuildable file generated from package and project state | may be regenerated |
| `templated-project-file` | file initially created from template, then project-owned | must not be overwritten silently |
| `project-owned-sot` | canonical project facts | never overwritten by package update without explicit migration |
| `derived-runtime-state` | cache, graph DB, MCP projection, runtime state | rebuildable from SoT |

This distinction is mandatory to prevent package updates from destroying project knowledge.

## Drift detection

Drift exists when installed asset expectations and project files disagree.

Examples:

- installed traceability profile expects `docs/traceability/index.md`, but file is missing;
- package version expects a column in `edges-map.md`, but project file uses older format;
- project context points to an entity registry that no longer exists;
- generated graph projection is stale relative to markdown SoT;
- package cache says asset is installed, but project inventory lacks it.

Drift detection should report findings before repair.

## Reconcile model

Reconcile is the controlled repair of installed asset environment.

Baseline flow:

```text
read installed inventory
  -> read package expectations
  -> scan project-local materialization
  -> detect drift
  -> propose repair plan
  -> apply safe repairs or require human approval
  -> verify environment state
```

Safe repairs may include regenerating derived runtime state or creating missing optional indexes from templates.

Unsafe repairs include overwriting project-owned SoT, deleting files, or rewriting accepted project facts.

## Relationship to project context entry system

[`project-context-entry-system`](./assets/project-context-entry-system/index.md) defines baseline project context files such as `AGENTS.md` and `project/` entry points.

Asset Environment Project Manager can extend project context with asset-specific context files, but should keep them project-owned and explicit.

Example:

```text
project/traceabilityContext.md
```

This file can point agents to:

```text
docs/traceability/index.md
docs/product/entities-map.md
docs/system_design/entities-map.md
docs/architecture/entities-map.md
```

## Relationship to traceability

For a future `traceability-system asset`, environment manager owns installation and materialization of the traceability structure.

It does not own actual entities, edges and traces.

Project docs own:

```text
docs/product/entities-map.md
docs/system_design/entities-map.md
docs/architecture/entities-map.md
docs/traceability/edges-map.md
docs/traceability/trace-map.md
```

Graph DB and MCP state remain derived runtime projections.

## Open questions

- What is the canonical installed asset inventory file path?
- Should lockfile live in `project/`, `.hypergraph/`, or another runtime directory?
- How should project-local overrides be represented?
- Which repairs can be automatic and which require human approval?
- How should package updates declare migrations for templated project files?

## Canonical invariants

- Asset environment management is project-local.
- Installed package source and project-owned SoT are different layers.
- Templated files become project-owned unless explicitly marked as generated projection.
- Drift must be reported before destructive repair.
- Reconcile must preserve project facts.
- Agent-facing context should expose installed asset entry points without requiring agents to know package internals.
