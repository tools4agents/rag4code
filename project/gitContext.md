# Git Context

## Root Repository

- Root repository path: `/home/anton-admin/Загрузки/develop/education/hyper-graph`
- Role: primary repository for HyperGraph code, documentation, migration work, and top-level project coordination.

## Nested Repositories

### `.kilocode/`

- Path: `.kilocode/`
- Current role: legacy Kilo configuration and Memory Bank repository.
- Git behavior: if changes are made inside `.kilocode/`, git commands must run inside `.kilocode/`.
- Migration note: this repository is being phased out in favor of `AGENTS.md`, `project/`, `operational_scope/`, and `.kilo/`.

### `hsm/`

- Path: `hsm/`
- Role: Hyper Stack Manager.
- Git behavior: if changes are made inside `hsm/`, git commands must run inside `hsm/`.

## Working Rules

- Run git commands in the repository that owns the changed files.
- Do not mix root-repo changes and nested-repo commits in one git context.
- Treat nested repository boundaries as explicit operational boundaries.
- When planning migrations, verify whether a file belongs to the root repository or to a nested repository before staging or committing.

## Current Migration State

- The root repository is moving away from legacy `.kilocode`-based context management.
- During migration, both legacy and new context layers may temporarily coexist.
- Until cleanup is complete, changes under `.kilocode/` should be treated as legacy-maintenance work, not as the target steady-state project layout.
