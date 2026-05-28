# HyperGraph Product Vision

> Status: Draft  
> Scope: product vision for HyperGraph  
> Role: product-level baseline for intent, users, value and direction

## Краткое видение

HyperGraph — это local-first engineering knowledge graph runtime для проектов, который помогает человеку и ИИ-агенту видеть, анализировать и поддерживать связи между engineering artifacts.

Первая итерация HyperGraph строит graph representation поверх Markdown-файлов внутри одного [`project`](../terms/project/terms/project.md): система индексирует Markdown Source of Truth, показывает incoming/outgoing links, affected files and impact reports, а также помогает безопасно выполнять операции с документацией.

Долгосрочно HyperGraph должен развиться от file-level documentation graph к typed engineering knowledge graph, где [`graph-node`](../terms/project/terms/graph-node.md) может представлять Markdown file, term, ADR, requirement, user story, scenario, test case, code artifact or project.

## Для чего создается продукт

HyperGraph создается, чтобы снять с ИИ-агента и человека рутинную, хрупкую и context-heavy работу по поддержанию связности проектного знания.

Без HyperGraph агент вынужден:
- искать backlinks через grep или regex;
- вручную вычислять relative paths;
- самостоятельно оценивать blast radius удаления или перемещения документа;
- удерживать global consistency большого documentation graph в контексте LLM;
- рисковать silent broken links в engineering Source of Truth.

HyperGraph переносит эту работу в deterministic graph/indexing runtime. ИИ-агент использует HyperGraph как инструмент, а не заменяет его алгоритмическую ответственность собственными эвристиками.

## Целевые пользователи

### ИИ-агент

Основной пользователь HyperGraph — ИИ-агент, который работает с project-local documentation and engineering artifacts через MCP interface.

Агенту нужны:
- быстрые incoming/outgoing link queries;
- machine-readable impact reports;
- affected files for semantic correction;
- safe move/rename support;
- deterministic graph traversal вместо ad-hoc repository search.

### Человек

Человек использует HyperGraph через CLI interface, чтобы:
- зарегистрировать и переиндексировать project;
- проверить graph state;
- увидеть affected files and impact reports;
- контролировать операции, которые могут затронуть Source of Truth.

## Product responsibility

HyperGraph отвечает за:
- ведение project-local derived graph representation;
- предоставление graph queries по indexed project state;
- выявление incoming/outgoing links;
- показ affected files для операций над artifacts;
- объяснимые reports для человека и агента;
- поддержку безопасных workflows вокруг documentation changes.

HyperGraph не отвечает за:
- Git version history;
- semantic rewriting текста;
- замену human/agent review;
- автоматическое понимание всех последствий branch/commit switch;
- IDE-specific user experience.

## Source of Truth и derived representation

В первой итерации project files под Git являются [`source-of-truth`](../terms/project/terms/source-of-truth.md) для содержимого проекта.

[`project-database`](../terms/project/terms/project-database.md) является [`derived-index`](../terms/project/terms/derived-index.md): она отражает текущий active filesystem/current commit state и может быть пересчитана из файлов.

Git owns versioning. Filesystem owns current project content. HyperGraph database reflects indexed current state.

После Git checkout или branch switch пользователь отвечает за manual reindex/rebuild.

## Graph direction

HyperGraph должен поддерживать representation, пригодную для:
- typed graph relations;
- traversal queries по ребрам;
- filtering by tags, [`file-type`](../terms/project/terms/file-type.md), [`semantic-type`](../terms/project/terms/semantic-type.md) and properties;
- future impact analysis across documentation, methodology, requirements, tests and code artifacts.

В первой итерации primary graph node — Markdown file. Term page может рассматриваться как Markdown file with semantic type `term`, но полноценный semantic artifact graph остается future direction.

## Product principles

- Filesystem remains human-readable and Git-versioned.
- Database is useful but disposable: it can be rebuilt from project files.
- Deterministic algorithms handle graph structure; semantic text correction belongs to humans or AI agents.
- Mutating or destructive workflows require explainable impact visibility.
- MCP and CLI are both first-class product interfaces.
- IDE integration is not a product goal for the first iteration.
