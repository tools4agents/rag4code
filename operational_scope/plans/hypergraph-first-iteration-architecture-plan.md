# Plan: HyperGraph First Iteration Architecture Work

> Status: Draft  
> Scope: HyperGraph first iteration Product/System/Architecture follow-up work  
> Role: operational plan for sequencing materialized tasks and preserving candidate follow-up tasks

## Цель

Зафиксировать план дальнейшей архитектурной проработки первой итерации HyperGraph после начальной фиксации Product/System/Architecture baseline в `docs/`.

План нужен, чтобы:
- сохранить последовательность ближайших задач;
- не потерять candidate follow-up tasks между сессиями;
- не превращать преждевременные направления в executable task artifacts до уточнения базовых решений;
- дать future agents понятный continuation context.

## Canonical references

- [`docs/product/index.md`](../../docs/product/index.md)
- [`docs/system_design/index.md`](../../docs/system_design/index.md)
- [`docs/architecture/index.md`](../../docs/architecture/index.md)
- [`docs/terms/project/terms-map.md`](../../docs/terms/project/terms-map.md)
- [`operational_scope/task-map.md`](../task-map.md)
- [`operational_scope/input/findings/architecture-findings.md`](../input/findings/architecture-findings.md)

## Current materialized taskset

Следующие задачи уже materialized under `HyperGraph First Iteration` in [`task-map.md`](../task-map.md):

1. [`hg-001-consolidate-design-docs-and-context-entry-navigation.md`](../tasks/hg-001-consolidate-design-docs-and-context-entry-navigation.md)
2. [`hg-002-define-project-config-schema.md`](../tasks/hg-002-define-project-config-schema.md)
3. [`hg-003-define-project-registry-and-database-binding-schemas.md`](../tasks/hg-003-define-project-registry-and-database-binding-schemas.md)
4. [`hg-004-design-project-lifecycle-operations.md`](../tasks/hg-004-design-project-lifecycle-operations.md)
5. [`hg-005-define-markdown-link-syntax-matrix.md`](../tasks/hg-005-define-markdown-link-syntax-matrix.md)
6. [`hg-006-define-link-resolution-and-root-safety-policy.md`](../tasks/hg-006-define-link-resolution-and-root-safety-policy.md)

## Phase 1 — Foundation tasks

Phase 1 should execute the six materialized tasks first.

Rationale:
- `hg-001` makes navigation reliable for future agents;
- `hg-002` and `hg-003` define the project/config/registry foundation;
- `hg-004` defines lifecycle operations that CLI/MCP contracts will later expose;
- `hg-005` and `hg-006` define the Markdown graph boundary required before parser, rewrite and report contracts.

Expected result:
- durable docs navigation is synchronized;
- project config schema is clear;
- registry/backend/binding schemas are conceptually clear;
- project lifecycle behavior is documented;
- Markdown link syntax matrix exists;
- link resolution and root safety policy exists.

## Phase 2 — Revalidation checkpoint

After `hg-001` through `hg-006`, perform a short design checkpoint.

Checkpoint goals:
- review which assumptions changed;
- update or reduce architecture findings;
- decide which candidate tasks should be materialized next;
- split, merge or discard candidate tasks based on Phase 1 outputs;
- avoid carrying obsolete speculative tasks into execution.

This checkpoint can be a short plan update, review artifact or direct task-map update if the next taskset is obvious.

## Candidate follow-up tasks

These candidates are intentionally not materialized as executable task artifacts yet. They must be revalidated after Phase 1.

### Parser strategy for Markdown MVP

Purpose:
- compare parser candidates;
- evaluate source range support;
- decide whether AST/token stream is sufficient;
- define parser spike or ADR path.

Depends on:
- `hg-005` Markdown link syntax matrix;
- `hg-006` link resolution/root safety policy.

### Move dry-run/apply safety model

Purpose:
- design operation plan model;
- decide plan id/token behavior;
- define stale file checks between dry-run and apply;
- define safe rewrite and partial failure boundaries.

Depends on:
- `hg-005`;
- `hg-006`;
- parser strategy direction.

### Remove impact report contract

Purpose:
- define affected files structure;
- define incoming references representation;
- decide snippets/ranges/severity;
- keep invariant: HyperGraph reports structural impact, agent/human handles semantic correction.

Depends on:
- `hg-005`;
- `hg-006`.

### Stale index policy

Purpose:
- decide file hash/mtime/indexed commit metadata;
- define query behavior on stale database;
- define freshness requirements for mutating operations;
- document branch/commit switch implications.

Depends on:
- `hg-003`;
- `hg-004`.

### Storage backend evaluation / ADR

Purpose:
- compare ArcadeDB, MongoDB/MongoDB Atlas and simpler alternatives;
- separate registry storage needs from graph database needs;
- decide whether first implementation needs graph DB, document DB or staged approach.

Depends on:
- `hg-003`;
- graph requirements from `hg-005` and `hg-006`.

### CLI command model

Purpose:
- design CLI command tree;
- define human-readable and JSON output modes;
- define project selection behavior;
- align CLI with lifecycle operations.

Depends on:
- `hg-004`.

### MCP tool contracts

Purpose:
- define MCP tool list and schemas;
- define project context passing;
- define structured reports and errors;
- define safeguards around mutating operations.

Depends on:
- `hg-004`;
- remove/move/report design tasks.

### Test design for first iteration graph safety

Purpose:
- define fixtures for Markdown links;
- test path resolution and root escape protection;
- test rewrite safety;
- test DB rebuild idempotency;
- test CLI/MCP consistency.

Depends on:
- `hg-005`;
- `hg-006`;
- move/remove/report contracts.

## Constraints

- Do not materialize candidate follow-up tasks until Phase 1 outputs are reviewed.
- Do not treat this plan as durable engineering SoT; accepted decisions must be reflected in `docs/`.
- Do not create implementation tasks before design baselines for config, registry, lifecycle and link resolution are clear.
- Keep `task-map.md` navigable as a router; avoid turning it into a large unstructured backlog.

## Open questions / risks

- `task-map.md` may need to become a thin router to per-scope task maps if the HyperGraph First Iteration scope grows.
- Candidate tasks may split further after the first six tasks, especially parser strategy, move safety and MCP contracts.
- Storage backend ADR may require a spike before decision.

## Status

- Current state: Phase 1 tasks materialized; candidate follow-up tasks preserved in this plan.
- Next step: execute or assign `hg-001`.
- Maturity: plan-stage, not executable taskset beyond `hg-001` through `hg-006`.
