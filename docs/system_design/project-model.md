# Project Model

> Status: Draft  
> Scope: system-level project model for HyperGraph  
> Role: external behavior and ownership boundaries for project-scoped operation

## Назначение

[`project`](../terms/project/terms/project.md) — основная system-level единица работы HyperGraph.

Все CLI and MCP operations выполняются в контексте выбранного project. Project задает локальную границу анализа, изоляцию graph state and project-specific configuration.

## Project composition

На первой итерации каждый project имеет:
- ровно один [`project-root`](../terms/project/terms/project-root.md);
- один [`project-config`](../terms/project/terms/project-config.md);
- одну изолированную [`project-database`](../terms/project/terms/project-database.md);
- набор project files внутри root, которые являются Source of Truth для indexed content.

```text
Project
  project-root
  project-config
  project-database
  project files
```

## Project root

Project root — это filesystem boundary для одного project context.

System behavior:
- HyperGraph индексирует files только внутри project root;
- paths внутри project нормализуются относительно project root;
- операции над files не должны выходить за root boundary;
- один project не имеет нескольких roots.

Project root не равен автоматически Git repository boundary: nested repositories внутри root могут существовать и по умолчанию считаются частью project scan, если не исключены config-ом.

## Project config

Project config управляет project-local behavior.

В первой итерации config должен поддерживать exclude rules: пользователь задает paths, которые HyperGraph не должен индексировать.

System behavior:
- excluded paths не попадают в indexing scope;
- excluded files не должны появляться как active graph nodes;
- `.git` hard-excluded всегда, даже если пользователь не указал это явно;
- шаблоны exclude rules для разных project types являются future capability, а не обязательной функцией первой итерации.

## Project database

Project database — это isolated derived database одного project.

System behavior:
- каждый project имеет собственную database;
- database не разделяется между projects;
- database can be rebuilt from project files;
- потеря database не является потерей project Source of Truth;
- stale database после внешних изменений project files требует reindex/rebuild.

## Multi-project model

HyperGraph может работать с несколькими projects как с изолированными contexts.

На первой итерации:
- каждый project имеет один root;
- каждый project имеет собственную database;
- operations выполняются внутри selected project;
- cross-project traversal не поддерживается;
- shared graph между projects не строится.

## Future cross-project model

В future scope project может стать graph node для cross-project links.

В такой модели один project видит другой project как external project node или black-box reference:
- связь между projects фиксируется как graph relation;
- target project определяется по project id;
- внутреннее устройство другого project не раскрывается в текущем project database;
- для детального анализа пользователь или агент переходит в target project context.

Эта модель не входит в первую итерацию и не должна влиять на MVP contracts.

## External actors

System-level actors первой итерации:
- человек через CLI;
- ИИ-агент через MCP;
- Git как external versioning system;
- local filesystem как holder current project files;
- project database как derived system state.

CLI and MCP являются interfaces к одной project-scoped system capability. Они не должны создавать разные interpretations project state.
