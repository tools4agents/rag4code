# Graph Model

> Status: Draft  
> Scope: system-level graph model for HyperGraph  
> Role: baseline model for graph nodes, classifications, relations and first-iteration boundaries

## Назначение

Этот документ фиксирует system-level модель graph representation HyperGraph.

Graph model должен поддерживать первую итерацию с Markdown file graph и при этом не закрывать путь к будущему engineering knowledge graph, где [`graph-node`](../terms/project/terms/graph-node.md) может представлять разные engineering artifacts.

## Базовая идея

HyperGraph строит graph representation поверх project files and derived metadata.

В первой итерации primary graph node — Markdown file. Future model допускает nodes для terms, ADR, requirements, user stories, scenarios, test cases, code artifacts and projects.

Graph representation должна быть пригодна для:
- typed graph relations;
- traversal queries по ребрам;
- filtering by tags, [`file-type`](../terms/project/terms/file-type.md), [`semantic-type`](../terms/project/terms/semantic-type.md) and properties;
- impact analysis and affected files discovery.

## Node identity layers

HyperGraph различает physical source classification and semantic classification.

### File type

[`file-type`](../terms/project/terms/file-type.md) описывает physical format/source file.

Examples:
- Markdown file: `*.md`;
- Python script/module: `*.py`;
- future source/documentation formats.

File type отвечает на вопрос: из какого physical artifact or file source извлечен graph node or graph data.

### Semantic type

[`semantic-type`](../terms/project/terms/semantic-type.md) описывает domain meaning graph node or extracted artifact.

Examples:
- `term`;
- `ADR`;
- `requirement`;
- `user-story`;
- `scenario`;
- `test-case`;
- `module`;
- `class`;
- `function`;
- `test-implementation`;
- `project`.

Semantic type отвечает на вопрос: какую engineering сущность представляет node.

## First iteration node model

В первой итерации HyperGraph использует file-level graph.

Primary node:

```text
MarkdownFile
  file_type = markdown
  semantic_type = optional classification
```

Minimal behavior:
- каждый indexed Markdown file может быть graph node;
- links между Markdown files формируют directed edges;
- incoming/outgoing link queries работают на file-level nodes;
- unsupported/unresolved/external links сохраняются как link records/statuses, но не обязательно создают active internal graph edges.

## Term pages in first iteration

Term page остается Markdown file, но может иметь semantic type `term`.

Это означает:
- physical node still comes from Markdown file;
- semantic classification marks this file as term page;
- term page может участвовать в file-level link graph как обычный Markdown file;
- полноценная term ontology and semantic relation model не является обязательной частью первой итерации.

Такой подход позволяет использовать [`terms-management-system asset`](../terms/project/terms/terms-management-system-asset.md) как source of semantic classification без преждевременного перехода к full semantic graph.

## Future artifact node model

Future graph model допускает, что один file может быть container for multiple semantic graph nodes.

Examples:
- Markdown file contains ADR and several decisions;
- Markdown file contains multiple requirements;
- Python file contains module, classes and functions;
- test file contains test implementations linked to documented test cases.

Future node examples:
- `Term`;
- `ADR`;
- `Requirement`;
- `UserStory`;
- `Scenario`;
- `TestCase`;
- `CodeArtifact`;
- `Project`.

This future model changes graph granularity from file-level to artifact-level, but does not invalidate first-iteration file graph.

## Relation model

First iteration relation:

```text
MarkdownFile --LINKS_TO--> MarkdownFile
```

`LINKS_TO` means resolved internal Markdown link from source file to target file.

Future relation types may include:
- `DEFINES`;
- `USES_TERM`;
- `IMPLEMENTS`;
- `VERIFIES`;
- `DEPENDS_ON`;
- `AFFECTS`;
- `DERIVED_FROM`;
- `REFERENCES_PROJECT`.

Future relations are not MVP requirements. They define the direction for representation capability and storage requirements.

## Project as future graph node

In future cross-project model, [`project`](../terms/project/terms/project.md) can appear as graph node.

System-level expectation:
- a project node represents another project as a black-box external entity;
- relation stores external project id and relationship metadata;
- current project database does not expand internal graph of target project;
- detailed traversal requires switching to target project context.

This is out of scope for first iteration.

## Boundaries

Graph model in this document is not:
- database schema;
- storage backend decision;
- parser implementation contract;
- full ontology for all future artifact types;
- execution plan.
