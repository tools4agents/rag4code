# Project Identity and Registry

> Status: Draft  
> Scope: system-level identity and registry model for HyperGraph projects  
> Role: boundary rules for project identity, local registration, registry records and database binding

## Назначение

Этот документ фиксирует system-level модель identity and registry для [`project`](../terms/project/terms/project.md) в HyperGraph.

Модель нужна, чтобы разделить portable project identity, local machine registration, project-local config, registry metadata and database binding.

## Hybrid model

HyperGraph использует hybrid model:

```text
project-local config
  <project-root>/.hypergraph/project.toml
  owns portable project identity and shared project settings

machine-local project registry
  owns local project registrations and runtime bindings

database backend configuration
  owns available database service connection/startup settings

project database binding
  maps project instance to logical project database
```

Эта модель позволяет шарить project-level настройки через Git и одновременно хранить machine-specific paths, service settings and local registrations outside project Source of Truth.

## Logical project identity

[`project-key`](../terms/project/terms/project-key.md) — portable logical identity проекта.

System behavior:
- `project-key` задается человеком в `.hypergraph/project.toml`;
- `project-key` переносится вместе с project-local config;
- `project-key` не должен генерироваться молча как единственная identity проекта;
- `project-key` может использоваться в future cross-project references;
- `project-key` не обязан быть globally unique без отдельной policy.

Example:

```toml
project_key = "hyper-graph"
display_name = "HyperGraph"
```

## Local project instance identity

[`project-instance-id`](../terms/project/terms/project-instance-id.md) — machine-local identifier конкретной регистрации project.

System behavior:
- создается при `project register`;
- хранится в [`project-registry`](../terms/project/terms/project-registry.md);
- отличает local clones and worktrees одного `project-key`;
- используется для local registry and database binding;
- не хранится как portable project identity в shared project config.

Example:

```text
project_key = "hyper-graph"
project_instance_id = "6f7c..."
root_path = "/data/develop/education/hyper-projects/hyper-graph"
```

## Project-local config

Project-local config lives at:

```text
<project-root>/.hypergraph/project.toml
```

System-level responsibilities:
- хранить `project-key`;
- хранить shared project settings;
- хранить scan/indexing conventions, включая excludes;
- быть удобным для sharing through Git;
- не хранить machine-specific credentials or local service connection secrets.

Project-local config is created by `project init` as a template. User fills required placeholders before `project register`.

## Project registry

`Project-registry` is machine-local.

System-level responsibilities:
- хранить registered project instances;
- связывать `project-instance-id` with root path;
- хранить path к project-local config;
- хранить indexing metadata;
- хранить [`project-database-binding`](../terms/project/terms/project-database-binding.md);
- ссылаться на available [`database-backend-config`](../terms/project/terms/database-backend-config.md) when needed.

Registry record should separate:
- project instance metadata;
- database binding;
- backend service configuration.

Registry storage backend is not fixed at System Design level. It may be JSON artifacts, document-oriented storage, MongoDB, MongoDB Atlas or another backend if machine-local registry semantics remain stable.

## Database backend config
[`database-backend-config`](../terms/project/terms/database-backend-config.md) describes available [`database-service`](../terms/project/terms/database-service.md) backends.

System-level responsibilities:
- define backend type;
- define local or managed mode;
- provide connection settings or references;
- provide Docker image/startup metadata for local services when applicable;
- allow one backend service to host several project databases.

Backend config is machine-local and should not be treated as project Source of Truth.

## Project database binding

`Project-database-binding` maps one `project-instance-id` to one logical [`project-database`](../terms/project/terms/project-database.md) inside selected database backend.

System-level responsibilities:
- select database backend for the project instance;
- define logical database name or namespace;
- store schema/index version metadata when needed;
- allow moving project database to another backend without changing `project-key`.

Binding is machine-local because it depends on user environment and selected backend.

## Init and register lifecycle

HyperGraph separates project initialization and local registration.

### `project init <root>`

Creates:

```text
<root>/.hypergraph/project.toml
```

Expected behavior:
- command creates a template with placeholders;
- user fills `project-key` and other required shared settings;
- command does not create local registry identity as the main outcome.

### `project register <root>`

Reads completed project-local config and registers a local instance.

Expected behavior:
- validates `.hypergraph/project.toml`;
- reads `project-key`;
- creates `project-instance-id`;
- creates or updates registry record;
- creates project database binding;
- associates binding with selected database backend config;
- may offer initial index/rebuild as a separate action.

## Clone, worktree and moved root behavior

If a repository is cloned elsewhere and contains `.hypergraph/project.toml`, it keeps the same `project-key` but receives a new `project-instance-id` on local registration.

If one machine has several clones/worktrees with the same `project-key`, each registration gets its own `project-instance-id` and its own project database binding.

If root path changes, MVP behavior may be unregister old instance and register new instance. A dedicated relink command is future convenience, not first-iteration requirement.

## Boundary

This model does not define:
- concrete registry storage backend;
- concrete database backend;
- final config schema;
- credential storage policy;
- cross-project reference protocol.
