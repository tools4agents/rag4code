# First Iteration Scope

> Status: Draft  
> Scope: first product iteration for HyperGraph  
> Role: product-level scope, MVP capabilities and non-goals

## Product frame

Первая итерация HyperGraph ограничена Markdown file graph внутри одного selected [`project`](../terms/project/terms/project.md).

Цель первой итерации — дать человеку и ИИ-агенту reliable graph visibility поверх Markdown Source of Truth: incoming links, outgoing links, affected files, impact reports and safe move workflow.

## In scope

### Project registration

Система должна позволять зарегистрировать `project` с одним [`project-root`](../terms/project/terms/project-root.md).

На первой итерации каждый project:
- имеет один root;
- имеет собственный [`project-config`](../terms/project/terms/project-config.md);
- имеет собственную [`project-database`](../terms/project/terms/project-database.md);
- изолирован от других projects.

### Project config and excludes

Project config должен поддерживать exclude rules для путей, которые HyperGraph не индексирует.

В первой итерации пользователь сам заполняет exclude rules. Шаблоны exclude rules для типовых проектов — future convenience capability.

Директория `.git` hard-excluded всегда.

### Markdown indexing

Система должна индексировать Markdown files внутри project root, кроме excluded paths.

Минимально система должна:
- найти Markdown files;
- извлечь supported Markdown links;
- нормализовать internal paths относительно project root;
- построить file-level graph;
- сохранить unresolved, external and unsupported link statuses.

### Incoming and outgoing links

Система должна предоставлять queries:
- какие Markdown files ссылаются на выбранный Markdown file;
- на какие Markdown files ссылается выбранный Markdown file.

Эти queries должны использовать indexed graph representation, а не требовать ad-hoc grep по repository.

### Affected files

Система должна показывать [`affected-file`](../terms/project/terms/affected-file.md) для операций, которые могут изменить или обесценить existing links.

Affected files нужны агенту и человеку как вход для semantic review and correction.

### Remove impact report

Первая итерация должна поддерживать remove impact report.

Remove impact report показывает:
- incoming references to the file planned for removal;
- files and locations that will be affected;
- links that may become broken;
- unsupported or unresolved cases.

Remove impact report не должен автоматически переписывать смысл текста. HyperGraph показывает structural impact; человек или ИИ-агент выполняет semantic correction.

### Move / rename workflow

Первая итерация должна поддерживать move/rename workflow для Markdown file.

Минимальный workflow:
1. dry-run показывает planned link rewrites;
2. report показывает affected files and skipped cases;
3. apply mode физически перемещает файл и обновляет safely rewriteable incoming links;
4. после операции graph state может быть rebuilt/reindexed.

### CLI and MCP interfaces

Первая итерация должна планироваться сразу с двумя first-class interfaces:
- CLI для человека;
- MCP для ИИ-агента.

Оба interfaces должны обращаться к одному product core и возвращать explainable outputs.

## Out of scope

Первая итерация не включает:
- automatic Git checkout/branch switch detection;
- automatic database rebuild after Git branch switch;
- cross-project graph traversal;
- semantic artifact graph inside Markdown files;
- code artifact extraction;
- automatic semantic rewriting of text;
- destructive remove rewrite by default;
- multi-root project model;
- shared database across projects.

## Future directions

Future product directions include:
- artifact-level graph nodes beyond Markdown files;
- term, ADR, requirement, user story, scenario, test case and code artifact nodes;
- project as graph node for cross-project links;
- templates for project exclude rules;
- LSP reconsideration for programming language source code artifact extraction;
- richer typed relations and traceability graph.

## First iteration success criteria

Первую итерацию можно считать успешной, если:
- человек может зарегистрировать project and reindex it;
- агент может получить incoming links без grep;
- агент может получить outgoing links для Markdown file;
- remove impact report показывает affected files and references;
- move dry-run показывает planned rewrites;
- move apply updates supported incoming Markdown links;
- database can be rebuilt from project files;
- branch/commit switch responsibility is explicit and belongs to user.
