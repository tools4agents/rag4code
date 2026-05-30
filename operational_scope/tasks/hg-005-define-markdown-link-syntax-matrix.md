# Task: Define Markdown MVP link syntax matrix

## Контекст

Первая итерация HyperGraph строит file-level graph по Markdown files. Core product value зависит от корректного извлечения, classification, resolution and safe rewrite Markdown links.

Связанные durable SoT artifacts:

- [`first-iteration-scope.md`](../../docs/product/first-iteration-scope.md);
- [`graph-model.md`](../../docs/system_design/graph-model.md);
- [`storage-and-indexing.md`](../../docs/architecture/storage-and-indexing.md);
- [`core-and-adapters.md`](../../docs/architecture/core-and-adapters.md);
- [`affected-file`](../../docs/terms/project/terms/affected-file.md);
- [`impact-report`](../../docs/terms/project/terms/impact-report.md).

Следующий unresolved design point — определить link syntax matrix для Markdown MVP: какие links поддерживаются, какие только распознаются/report-ятся, какие ignored, и какие остаются future scope.

## Цель

Сформировать MVP Markdown link syntax matrix, которая задает parser/link extraction scope, link resolution expectations and safe rewrite boundaries для first iteration.

## Scope

Включить classification для:

- inline Markdown links: `[text](path.md)`;
- links with title: `[text](path.md "title")`;
- anchors: `[text](path.md#section)`;
- same-file anchors: `[text](#section)`;
- reference links: `[text][id]` and `[id]: path.md`;
- shortcut/collapsed reference links;
- image links: `![alt](path.png)`;
- links to non-Markdown assets;
- external URLs;
- absolute paths;
- root-relative paths, if supported;
- extensionless links;
- directory links;
- paths with spaces and URL encoding;
- Obsidian/wiki links: `[[note]]`, `[[path|alias]]`;
- malformed or unsupported link syntax.

Для каждого link type определить:

- MVP status: supported / detected-only / ignored / unsupported / future;
- whether it can create `LINKS_TO` edge;
- whether it can appear in incoming/outgoing queries;
- whether it is safe rewriteable during move;
- what should be reported in impact report;
- what parser/source range information is required.

## Non-scope

Не включать:

- final parser library decision;
- full path resolution policy;
- symlink/root escape policy;
- implementation code;
- complete rewrite algorithm;
- MCP/CLI contract schemas;
- semantic graph or term ontology design.

## Expected durable docs updates

Создать или обновить focused Architecture/System doc.

Кандидаты:

```text
docs/architecture/markdown-link-syntax-matrix.md
docs/system_design/markdown-link-behavior.md
```

Если документ primarily determines parser/rewrite architecture, prefer `docs/architecture/`. If it primarily defines externally visible supported behavior, add system-level summary or link from System Design.

## Шаги реализации

- [ ] Прочитать current SoT по first iteration scope, graph model and storage/indexing.
- [ ] Составить list of Markdown link types relevant to MVP.
- [ ] Для каждого link type определить MVP status.
- [ ] Определить какие link types создают internal `LINKS_TO` edges.
- [ ] Определить какие link types должны появляться в reports but not in graph edges.
- [ ] Определить initial safe rewrite boundary for move.
- [ ] Определить parser/source range requirements.
- [ ] Зафиксировать unsupported/future cases explicitly.
- [ ] Обновить durable docs.

## Definition of Done

- [ ] Markdown link syntax matrix exists in durable docs.
- [ ] Supported MVP link types are explicit.
- [ ] Detected-only/unsupported/future link types are explicit.
- [ ] Graph edge creation rules are explicit for link types.
- [ ] Safe rewrite eligibility is explicit at matrix level.
- [ ] Impact report expectations are explicit for unsupported/unresolved links.
- [ ] Parser/source range requirements are identified.
- [ ] Matrix does not choose final parser library.
- [ ] Matrix does not fully define path resolution/root safety policy, except where needed to classify links.

## Execution Status

- Current State: queued
- Next Step: Build MVP link syntax matrix and materialize it in durable Architecture/System docs.
- Blockers: none
- Verification: Read updated docs and check consistency with graph model, storage/indexing and first-iteration scope.
