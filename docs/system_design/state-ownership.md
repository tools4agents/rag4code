# State Ownership

> Status: Draft  
> Scope: system-level state ownership for HyperGraph  
> Role: boundary rules for Git, filesystem, project files and derived database

## Назначение

Этот документ фиксирует, кому принадлежит state в HyperGraph system model.

Главный принцип первой итерации:

```text
Git owns versioning.
Filesystem owns current project content.
Project files are Source of Truth.
HyperGraph database reflects indexed current state.
```

## Git ownership

Git является external versioning system для project files.

Git отвечает за:
- commit history;
- branches;
- checkout;
- merge/rebase effects;
- rollback of files;
- versioned project content.

HyperGraph не отвечает за Git version history и не заменяет Git.

## Filesystem ownership

Local filesystem хранит current project files.

В первой итерации HyperGraph работает с active filesystem/current commit state: он индексирует то состояние файлов, которое находится в selected project root на момент indexing/reindexing.

Filesystem является operational source для rebuild derived graph representation.

## Project files as Source of Truth

Project files под Git являются [`source-of-truth`](../terms/project/terms/source-of-truth.md) для содержимого проекта.

Для первой итерации это означает:
- Markdown files являются first-class project files;
- database не должна становиться authoritative вместо files;
- graph state должен быть восстановим из files;
- human-readable files remain usable without HyperGraph database.

## Database as derived index

[`project-database`](../terms/project/terms/project-database.md) является [`derived-index`](../terms/project/terms/derived-index.md).

Database отвечает за:
- cached graph representation;
- incoming/outgoing link queries;
- traversal and filtering support;
- impact report data;
- ускорение CLI and MCP operations.

Database не отвечает за:
- Git history;
- authoritative project content;
- semantic rewriting decisions;
- long-term truth beyond indexed filesystem state.

## Branch and commit switch behavior

HyperGraph database reflects the active current filesystem/current commit state that was last indexed.

Если пользователь выполняет Git checkout, branch switch, merge, rebase или другой external Git operation, HyperGraph не обязан автоматически перестраивать database в первой итерации.

После таких операций пользователь отвечает за manual reindex/rebuild.

Expected behavior:
- system may expose explicit reindex/rebuild command;
- system may report stale or suspicious state if detectable;
- system must not claim Git-aware consistency without rebuild;
- automatic Git transition detection is out of scope for the first iteration.

## External file changes

Если project files изменены outside HyperGraph через editor, shell, Git or another tool, database может стать stale.

В первой итерации acceptable behavior:
- user manually triggers reindex/rebuild;
- operations can require fresh index before mutating files;
- reports should be based on known indexed state and should not silently pretend to include unindexed changes.

Detailed stale-index detection policy belongs to later System/Architecture Design.

## Mutating operations

HyperGraph mutating operations must respect ownership boundaries:
- file content changes are written to project files only when operation explicitly applies changes;
- database is updated or rebuilt after filesystem mutation;
- impact reports can be produced without mutating project files;
- semantic text correction remains responsibility of human or AI agent.

Remove impact report is read-only by default: it shows structural consequences and affected files, but does not rewrite semantic content.
