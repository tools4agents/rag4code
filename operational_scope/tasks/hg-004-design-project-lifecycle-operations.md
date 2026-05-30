# Task: Design project lifecycle CLI/MCP operations

## Контекст

Для первой итерации HyperGraph уже зафиксированы:

- [`project`](../../docs/terms/project/terms/project.md) как system-level единица работы;
- [`project-key`](../../docs/terms/project/terms/project-key.md) как portable logical identity;
- [`project-instance-id`](../../docs/terms/project/terms/project-instance-id.md) как local registration identity;
- [`project-registry`](../../docs/terms/project/terms/project-registry.md) как machine-local registry;
- [`project-database-binding`](../../docs/terms/project/terms/project-database-binding.md) как связь project instance с logical database;
- TOML config path `<project-root>/.hypergraph/project.toml`.

Связанные durable SoT artifacts:

- [`project-model.md`](../../docs/system_design/project-model.md);
- [`project-identity-and-registry.md`](../../docs/system_design/project-identity-and-registry.md);
- [`project-config-format.md`](../../docs/system_design/project-config-format.md);
- [`core-and-adapters.md`](../../docs/architecture/core-and-adapters.md);
- [`project-registry-and-database-service.md`](../../docs/architecture/project-registry-and-database-service.md).

Следующий unresolved design point — определить project lifecycle operations, которые будут доступны человеку через CLI и агенту через MCP или внутренние application ports.

## Цель

Спроектировать first-iteration lifecycle operations для project init/register/unregister/list/select/reindex, включая system behavior, inputs/outputs, state transitions and failure cases.

## Scope

Включить:

- `project init <root>` behavior;
- `project register <root>` behavior;
- `project unregister` behavior;
- `project list` behavior;
- project selection / active project context behavior;
- `project reindex` / rebuild behavior;
- expected lifecycle states;
- relationship to `.hypergraph/project.toml`;
- relationship to project registry;
- relationship to project database binding;
- behavior for moved/deleted root;
- behavior for clone/worktree with same `project-key`;
- human CLI expectations;
- AI-agent/MCP expectations at conceptual level.

## Non-scope

Не включать:

- final CLI command syntax freeze;
- final MCP tool schemas;
- registry/backend concrete schemas;
- project TOML schema details;
- storage backend decision;
- implementation code;
- cross-project reference protocol.

## Expected durable docs updates

Обновить или создать focused docs under `docs/system_design/` and/or `docs/architecture/`.

Кандидаты:

```text
docs/system_design/project-lifecycle.md
docs/architecture/project-lifecycle-operations.md
```

Если material is mostly externally visible behavior, prefer System Design. If operation routing through core/ports/adapters becomes central, add Architecture handoff section or focused Architecture doc.

## Шаги реализации

- [ ] Прочитать current SoT по project model, identity/registry and core/adapters.
- [ ] Описать lifecycle states for uninitialized/initialized/registered/indexed/stale/unregistered as needed.
- [ ] Описать `project init <root>` behavior and outputs.
- [ ] Описать `project register <root>` behavior and outputs.
- [ ] Описать unregister behavior and DB handling boundaries.
- [ ] Описать list/select active project behavior.
- [ ] Описать reindex/rebuild behavior.
- [ ] Описать expected failure cases and user-facing errors at design level.
- [ ] Разделить CLI/MCP conceptual operations without freezing exact contracts.
- [ ] Обновить durable docs.

## Definition of Done

- [ ] Project lifecycle states are documented or explicitly declared unnecessary.
- [ ] `project init` behavior is documented.
- [ ] `project register` behavior is documented.
- [ ] Unregister behavior is documented, including DB/binding handling boundary.
- [ ] Project list/select behavior is documented.
- [ ] Reindex/rebuild behavior is documented.
- [ ] Moved root / missing root behavior is documented.
- [ ] Clone/worktree behavior with same `project-key` remains consistent with `project-instance-id` model.
- [ ] CLI and MCP conceptual expectations are separated from final contracts.
- [ ] Documentation does not accidentally decide final CLI/MCP schemas.

## Execution Status

- Current State: queued
- Next Step: Design lifecycle operations and update System/Architecture docs.
- Blockers: none
- Verification: Read updated docs and check consistency with identity, registry and config format docs.
