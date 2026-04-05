# Repository Map

## Purpose

This file is a navigation map of the repository contents. It explains what lives where, without redefining architecture or git ownership rules.

## Top-Level Areas

- `services/` - implementation of independent services and MCP-oriented components.
- `hsm/` - Hyper Stack Manager sources and related orchestration assets.
- `docs/` - long-lived engineering documentation, principles, ADRs, contracts, and methodology documentation.
- `project/` - durable project context for humans and agents.
- `assets/` - methodology references, imported guidance, and support materials.
- `tools/` - project tooling and helper utilities.
- `packages/` - shared packages and reusable code artifacts.
- `src/` - root-level source code.

## Documentation Navigation

- Start with `docs/principles.md` for project values.
- Use `docs/methodology-layer/overview.md` as the entry point into methodology runtime documentation.
- Use `docs/contracts/README.md` to understand contract-layer boundaries.
- Use `docs/adr/` for recorded architectural decisions.

## Execution-layer navigation

- `operational_scope/` is the execution layer for the current iteration.
- `operational_scope/task-map.md` is the task index for active execution tasks.
- `operational_scope/ideas/`, `operational_scope/plans/`, `operational_scope/research/`, `operational_scope/discussion/`, and `operational_scope/tasks/` host the migrated operational artifacts.

## Kilo-Specific Navigation

- Legacy Kilo artifacts currently live in `.kilocode/`.
- Target Kilo-specific project configuration will live in `.kilo/` with `kilo.json`.

## Related Files

- `project/gitContext.md` for repository ownership and git boundaries.
- `project/techContext.md` for technical baseline.
- `project/context-migration.md` for the current migration direction.
