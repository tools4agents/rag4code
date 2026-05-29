# Project Registry and Database Service

> Status: Draft  
> Scope: architecture baseline for HyperGraph registry and database backend integration  
> Role: internal structure for registry storage, backend configuration and project database binding

## Назначение

Этот документ фиксирует architecture-level baseline для [`project-registry`](../terms/project/terms/project-registry.md), [`database-service`](../terms/project/terms/database-service.md), [`database-backend-config`](../terms/project/terms/database-backend-config.md) и [`project-database-binding`](../terms/project/terms/project-database-binding.md).

System-level identity rules, зафиксированные в [`project-identity-and-registry.md`](../system_design/project-identity-and-registry.md), остаются authoritative для externally visible behavior. Этот документ описывает internal architecture boundaries и responsibilities интеграции с backend.

## Architecture separation

HyperGraph не должен сворачивать registry, backend configuration и project database binding в один объект.

Architecture baseline:

```text
Project registry
  owns local project instance records
  owns project-database-binding records

Database backend config store
  owns available database-service configurations

Database service
  runtime backend/engine
  hosts one or many logical project databases

Storage adapter
  resolves binding + backend config
  executes graph/index operations
```

Такое разделение позволяет одному backend service обслуживать много project databases и менять backend connection settings без переписывания каждой project registration.

## Registry storage

Registry storage является machine-local и хранит registered project instances.

Candidate registry storage backends:
- JSON artifacts;
- document-oriented local storage;
- MongoDB;
- MongoDB Atlas;
- другой configurable backend, который сохраняет machine-local registry semantics.

Architecture constraints:
- registry backend должен поддерживать structured documents;
- registry records должны быть queryable by `project-instance-id`;
- registry не должен быть project Source of Truth;
- registry не должен хранить content project files;
- registry не должен смешивать backend service config с project instance records.

Final registry backend selection относится к будущему architecture decision.

## Форма registry record

Conceptual registry record:

```json
{
  "project_instance_id": "uuid",
  "project_key": "hyper-graph",
  "root_path": "/path/to/project",
  "config_path": "/path/to/project/.hypergraph/project.toml",
  "database_binding_id": "binding-uuid",
  "index_state": {
    "last_indexed_at": "...",
    "last_indexed_git_commit": "optional"
  }
}
```

Это conceptual shape, а не final schema.

## Database backend config

Database backend config описывает available runtime backends.

Conceptual backend config:

```json
{
  "database_backend_id": "local-arcadedb",
  "backend_type": "arcadedb",
  "mode": "docker",
  "connection": {
    "uri": "http://localhost:2480"
  },
  "startup": {
    "docker_image": "arcadedata/arcadedb:latest",
    "container_name": "hypergraph-arcadedb"
  },
  "capabilities": ["graph", "typed_edges", "traversal"]
}
```

Managed backend example:

```json
{
  "database_backend_id": "mongo-atlas-main",
  "backend_type": "mongodb",
  "mode": "managed",
  "connection": {
    "uri_env": "HYPERGRAPH_MONGO_ATLAS_URI"
  }
}
```

Credentials должны передаваться через references, а не копироваться в project-local config.

## Project database binding

Project database binding связывает один project instance с одной logical database или namespace внутри selected backend.

Conceptual binding:

```json
{
  "binding_id": "binding-uuid",
  "project_instance_id": "project-instance-uuid",
  "database_backend_id": "local-arcadedb",
  "database_name": "hypergraph_project_instance_uuid",
  "schema_version": "0.1.0"
}
```

Architecture constraints:
- binding не должен дублировать connection settings;
- binding не должен содержать Docker startup metadata;
- binding может измениться, если project database переносится на другой backend;
- изменение binding не должно менять `project-key`.

## Database service runtime

Database service — это runtime backend, который выполняет storage operations.

Supported deployment modes могут включать:
- local Docker container;
- local service, installed by user;
- managed cloud service;
- future embedded mode, если он будет выбран через ADR.

Architecture constraints:
- HyperGraph core не должен напрямую зависеть от Docker или managed service APIs;
- service startup/health checks принадлежат infrastructure/service management layer или adapter;
- storage adapter должен получать resolved connection information;
- backend-specific logic должна оставаться за storage/backend adapters.

## Storage adapter resolution flow

Когда CLI или MCP operation требует access к project database:

1. Resolve project registry record by `project-instance-id` или selected project.
2. Прочитать `project-database-binding` from registry.
3. Resolve `database-backend-config` by backend id.
4. Проверить, что database service reachable, или вернуть service unavailable report.
5. Использовать storage adapter for backend type.
6. Открыть logical database или namespace from binding.
7. Выполнить graph/index operation.

```text
project-instance-id
  -> project-registry record
  -> project-database-binding
  -> database-backend-config
  -> database-service
  -> logical project-database
```

## Backend flexibility

Architecture должна позволять разным пользователям выбирать разные backends.

Examples:
- developer A использует local Docker ArcadeDB;
- developer B использует MongoDB Atlas;
- CI использует ephemeral local backend;
- future production-like setup использует другой graph-capable service.

Эта гибкость не должна менять project-local `project-key` или project files Source of Truth.

## Boundaries

Этот документ не принимает решения по следующим вопросам:
- final registry storage backend;
- final graph database backend;
- exact document schemas;
- credential storage mechanism;
- Docker orchestration implementation;
- cloud provider integration.
