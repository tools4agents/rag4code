# Project Config Format

> Status: Draft  
> Scope: product/system-level note for HyperGraph project-local config format  
> Role: decision note for `.hypergraph/project.toml`, config ownership and format boundaries

## Назначение

Этот документ фиксирует product/system-level решение: project-local config HyperGraph должен храниться в TOML-файле внутри project root.

Canonical path:

```text
<project-root>/.hypergraph/project.toml
```

Этот файл является shared project-local config: он описывает portable identity and shared settings проекта и может быть shared через Git.

## Product rationale

HyperGraph должен быть удобен для командной работы с project-local knowledge graph.

Project-local config нужен, чтобы:
- хранить [`project-key`](../terms/project/terms/project-key.md) как portable logical identity;
- задавать shared scan/indexing conventions;
- фиксировать project-level exclude rules;
- позволить разработчикам видеть and review project configuration as normal text file;
- переносить базовые настройки вместе с repository.

TOML выбран как human-edited config format, потому что он:
- хорошо читается человеком;
- поддерживает comments;
- хорошо подходит для секций и списков;
- менее хрупок для ручного редактирования, чем JSON;
- менее неоднозначен, чем YAML;
- привычен для project configuration через `pyproject.toml`, `Cargo.toml` and similar files.

## System-level ownership

`.hypergraph/project.toml` принадлежит project-local config layer.

Он должен хранить shared configuration:
- `project_key`;
- display name or description;
- scan/indexing conventions;
- exclude rules;
- future project-level graph conventions.

Он не должен хранить machine-local secrets or service-specific credentials.

Machine-local runtime settings belong to [`project-registry`](../terms/project/terms/project-registry.md), [`database-backend-config`](../terms/project/terms/database-backend-config.md) and local environment-specific configuration.

## Minimal conceptual shape

Initial template may look like:

```toml
project_key = "<fill-project-key>"
display_name = "<fill-display-name>"

[scan]
exclude = [
  ".venv/",
  "node_modules/",
  "dist/",
  "build/"
]
```

`.git` does not have to be listed: it is hard-excluded by HyperGraph regardless of project config.

This is a conceptual shape, not the final config schema.

## Init/register relation

`project init <root>` creates `.hypergraph/project.toml` as a template with placeholders.

The user fills required values manually before registration.

`project register <root>` reads completed `.hypergraph/project.toml`, validates it and creates machine-local registration in the project registry.

This separates:
- project-local shared identity and settings;
- local machine registration;
- database backend selection;
- project database binding.

## JSON-compatible artifacts boundary

TOML is chosen for human-edited project-local config.

JSON-compatible documents remain appropriate for:
- registry records;
- MCP tool inputs and outputs;
- machine-readable impact reports;
- API responses;
- backend configuration documents if stored in document-oriented storage.

This split keeps human-edited config readable while preserving structured machine-readable contracts for interfaces and registry storage.

## Out of scope

This document does not define:
- final TOML schema;
- validation rules for every field;
- credential storage policy;
- local override format;
- exact registry document schemas.
