# Future Capabilities

> Status: Draft  
> Scope: product-level future capability directions for HyperGraph  
> Role: preserve strategic product direction beyond first iteration without turning it into MVP scope

## Назначение

Этот документ фиксирует future product directions, которые важны для long-term HyperGraph vision, но не входят в first iteration scope.

Он нужен, чтобы future capabilities не потерялись и одновременно не стали скрытыми MVP requirements.

## Engineering artifact graph

Long-term HyperGraph должен развиться от Markdown file graph к engineering artifact graph.

Future graph nodes may represent:
- term;
- ADR;
- requirement;
- user story;
- scenario;
- test case;
- code artifact;
- project.

Product value:
- видеть не только file links, но и engineering dependencies;
- поддерживать traceability from intent to implementation and tests;
- строить impact analysis по typed artifact relations;
- помогать ИИ-агенту понимать blast radius изменения на уровне engineering meaning.

## Semantic classification

Future HyperGraph должен использовать semantic classification поверх physical file sources.

Examples:
- Markdown file with semantic type `term`;
- Markdown file with semantic type `ADR`;
- Python file containing module, class, function or test implementation;
- project node representing external project relation.

Product value:
- filtering by semantic type;
- artifact-aware navigation;
- более точный impact report;
- основа для traceability graph.

## Traceability graph

Traceability graph должен позволять связывать engineering artifacts typed relations.

Candidate relation examples:
- requirement `VERIFIED_BY` test case;
- user story `REALIZED_BY` requirement or scenario;
- ADR `AFFECTS` service or code artifact;
- test case `IMPLEMENTED_BY` test implementation;
- term `USED_BY` documentation or code artifact.

Эта capability требует отдельного Product/System/Architecture design и не входит в первую итерацию.

## Code artifact graph

Future HyperGraph может индексировать programming language source code artifacts.

Candidate node types:
- module;
- class;
- function;
- method;
- test implementation.

LSP не нужен для Markdown MVP, но может быть снова рассмотрен как possible source-code intelligence mechanism для programming language artifacts.

## Cross-project graph

Future HyperGraph может поддержать cross-project links через project node model.

Product direction:
- каждый project остается isolated context with its own database;
- external project может быть представлен как black-box project node;
- relation содержит project id and interaction metadata;
- пользователь или агент может перейти в target project context для детального анализа.

Cross-project traversal and shared project graph не входят в первую итерацию.

## Exclude rule templates

Future HyperGraph может предлагать templates для project exclude rules, аналогично тому, как GitHub предлагает `.gitignore` templates.

Candidate templates:
- Python project;
- Node.js project;
- documentation-only project;
- monorepo-like project;
- generated-docs-heavy project.

В первой итерации пользователь сам задает exclude rules; `.git` hard-excluded always.

## Boundary

Capabilities in this document are not:
- first iteration requirements;
- architecture decisions;
- implementation tasks;
- storage backend commitments.
