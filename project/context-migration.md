# Context Migration

## Purpose

This file records the current repository-level migration from legacy `.kilocode`-based context management to the new layered context model.

## Migration Direction

The target model is:

- `AGENTS.md` as the navigation contract;
- `project/` as durable project context;
- `docs/` as engineering Source of Truth;
- `operational_scope/` as temporary execution layer;
- `.kilo/` and `kilo.json` as Kilo-specific configuration.

## Current State

- Legacy context still exists in `.kilocode/`.
- Legacy execution artifacts have been moved into `operational_scope/`.
- Long-lived engineering documentation already exists in `docs/`.
- New root-level `AGENTS.md` and `project/` are being introduced as the first migration step.
- Temporary operational artifacts from `docs/idea/`, `docs/plans/`, and `docs/specification/` are being migrated into `operational_scope/`.

## Migration Boundaries

- Do not move architecture canon into `project/`.
- Do not move temporary execution status into `docs/`.
- Do not treat `.kilocode/` as the target steady-state layout.
- Prefer moving Kilo-specific operational rules into `.kilo/rules/` rather than expanding `AGENTS.md`.
- Move temporary `idea`, `plan`, and `discussion` artifacts out of `docs/` into `operational_scope/` unless they are explicitly promoted into canonical documentation.

## Expected Next Steps

- Introduce `operational_scope/` and its task map.
- Introduce `.kilo/` and `kilo.json`.
- Move legacy Kilo-specific rules into `.kilo/rules/`.
- Review and remove any remaining references to the old execution-layer layout.
- Phase out `.kilocode/` after the new structure becomes self-sufficient.
