# Task: Define link resolution and root safety policy

## Контекст

Первая итерация HyperGraph строит Markdown file graph внутри одного [`project-root`](../../docs/terms/project/terms/project-root.md). Для корректных incoming/outgoing queries, move/rename workflow and impact reports нужно явно определить link resolution semantics and root safety policy.

Связанные durable SoT artifacts:

- [`first-iteration-scope.md`](../../docs/product/first-iteration-scope.md);
- [`project-model.md`](../../docs/system_design/project-model.md);
- [`graph-model.md`](../../docs/system_design/graph-model.md);
- [`state-ownership.md`](../../docs/system_design/state-ownership.md);
- [`storage-and-indexing.md`](../../docs/architecture/storage-and-indexing.md);
- [`core-and-adapters.md`](../../docs/architecture/core-and-adapters.md);
- [`project-root`](../../docs/terms/project/terms/project-root.md);
- [`affected-file`](../../docs/terms/project/terms/affected-file.md).

Связанная queued task:

- [`hg-005-define-markdown-link-syntax-matrix.md`](./hg-005-define-markdown-link-syntax-matrix.md)

## Цель

Спроектировать policy для resolution Markdown links в canonical project-relative targets and for protecting project root boundary during indexing and mutating operations.

## Scope

Включить:

- canonical project-relative path model;
- handling of `.` and `..` path segments;
- relative paths from source Markdown file;
- absolute paths and root-relative paths policy;
- links that point outside project root;
- symlink handling policy;
- `.git` hard-exclude interaction;
- excluded paths interaction;
- case sensitivity assumptions;
- URL encoding and spaces in paths at policy level;
- missing target / unresolved classification;
- duplicate candidate target behavior;
- directory target behavior at policy level;
- root escape prevention for indexing and move/apply;
- post-resolution statuses used by graph/index/reporting.

## Non-scope

Не включать:

- full Markdown link syntax matrix details;
- final parser library decision;
- complete rewrite algorithm;
- CLI/MCP contract schemas;
- storage backend decision;
- implementation code;
- full security sandbox design beyond path/root safety.

## Expected durable docs updates

Создать или обновить focused Architecture/System doc.

Кандидаты:

```text
docs/architecture/link-resolution-and-root-safety.md
docs/system_design/link-resolution-behavior.md
```

Если policy primarily defines externally visible behavior and safety boundary, include System Design summary. If it defines algorithms and canonicalization flow, include Architecture doc.

## Шаги реализации

- [ ] Прочитать current SoT по project root, graph model and storage/indexing.
- [ ] Согласовать boundary with Markdown link syntax matrix task.
- [ ] Определить canonical project-relative path representation.
- [ ] Описать path normalization and root containment checks.
- [ ] Описать symlink policy.
- [ ] Описать excluded paths behavior.
- [ ] Описать resolution statuses and failure categories.
- [ ] Описать case sensitivity and URL encoding assumptions.
- [ ] Описать root escape behavior for indexing and mutating operations.
- [ ] Обновить durable docs.

## Definition of Done

- [ ] Canonical project-relative target model is documented.
- [ ] Root containment and root escape policy is explicit.
- [ ] `.` / `..` normalization behavior is explicit.
- [ ] Symlink policy is explicit or explicitly deferred with safe default.
- [ ] Excluded path behavior is explicit.
- [ ] Resolution statuses are documented.
- [ ] Missing/duplicate/directory target behavior is covered at policy level.
- [ ] Case sensitivity and URL encoding assumptions are documented or explicitly deferred.
- [ ] Policy does not choose final parser library.
- [ ] Policy remains consistent with Markdown link syntax matrix and first-iteration scope.

## Execution Status

- Current State: queued
- Next Step: Design resolution/root safety policy and materialize it in durable Architecture/System docs.
- Blockers: none
- Verification: Read updated docs and check consistency with project root, graph model, storage/indexing and Markdown link syntax matrix.
