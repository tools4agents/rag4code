# Task: Define project registry and database binding schemas

## Контекст

Для первой итерации HyperGraph уже зафиксирована hybrid model:

- project-local config хранит portable [`project-key`](../../docs/terms/project/terms/project-key.md);
- machine-local [`project-registry`](../../docs/terms/project/terms/project-registry.md) хранит local project registrations;
- [`database-backend-config`](../../docs/terms/project/terms/database-backend-config.md) описывает available database services;
- [`project-database-binding`](../../docs/terms/project/terms/project-database-binding.md) связывает local project instance с logical [`project-database`](../../docs/terms/project/terms/project-database.md).

Связанные durable SoT artifacts:

- [`project-identity-and-registry.md`](../../docs/system_design/project-identity-and-registry.md);
- [`project-registry-and-database-service.md`](../../docs/architecture/project-registry-and-database-service.md);
- [`storage-and-indexing.md`](../../docs/architecture/storage-and-indexing.md);
- [`project-instance-id`](../../docs/terms/project/terms/project-instance-id.md);
- [`database-service`](../../docs/terms/project/terms/database-service.md).

Следующий unresolved design point — определить conceptual schemas для registry record, database backend config and project database binding without prematurely choosing final storage backend.

## Цель

Спроектировать conceptual JSON/BSON-compatible schemas для machine-local project registry, database backend config and project database binding, достаточные для дальнейшего design of project lifecycle operations and storage adapter resolution flow.

## Scope

Включить:

- conceptual schema for project registry record;
- conceptual schema for `database-backend-config`;
- conceptual schema for `project-database-binding`;
- required/optional fields;
- relationship between `project-instance-id`, `project-key`, root path, config path and binding;
- database backend id and logical database name/namespace rules;
- index metadata fields, including optional last indexed commit;
- credentials reference boundary;
- Docker startup metadata boundary;
- managed backend / local backend distinctions;
- JSON/BSON compatibility expectations.

## Non-scope

Не включать:

- final registry storage backend decision;
- final graph database backend decision;
- project-local TOML schema;
- credential storage implementation;
- Docker orchestration implementation;
- MCP/CLI command contracts;
- production database schema/migrations;
- implementation code.

## Expected durable docs updates

Минимально обновить:

- [`docs/architecture/project-registry-and-database-service.md`](../../docs/architecture/project-registry-and-database-service.md)

При необходимости создать focused doc:

```text
docs/architecture/registry-and-database-binding-schemas.md
```

Contract-level materialization можно отложить, если schemas еще conceptual и не готовы стать formal contracts.

## Шаги реализации

- [ ] Прочитать current SoT по project identity, registry and database service.
- [ ] Определить conceptual project registry record schema.
- [ ] Определить conceptual database backend config schema.
- [ ] Определить conceptual project database binding schema.
- [ ] Разделить fields между registry record, backend config and binding.
- [ ] Зафиксировать required and optional fields.
- [ ] Зафиксировать secrets/credentials boundary as references, not inline secrets.
- [ ] Зафиксировать local Docker backend and managed backend examples.
- [ ] Зафиксировать JSON/BSON compatibility assumptions.
- [ ] Обновить durable docs.

## Definition of Done

- [ ] Registry record conceptual schema is documented.
- [ ] Database backend config conceptual schema is documented.
- [ ] Project database binding conceptual schema is documented.
- [ ] Fields are not duplicated across registry/backend/binding layers without explicit reason.
- [ ] Credential handling boundary is explicit.
- [ ] Docker startup metadata belongs to backend config, not binding.
- [ ] Binding maps project instance to logical database/namespace, not to full connection settings.
- [ ] JSON/BSON compatibility expectations are clear.
- [ ] Documentation does not choose final registry or graph DB backend.

## Execution Status

- Current State: queued
- Next Step: Design conceptual schemas and update architecture docs.
- Blockers: none
- Verification: Read updated docs and check consistency with `project-registry`, `database-backend-config`, `project-database-binding` term pages.
