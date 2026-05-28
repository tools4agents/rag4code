# derived-index

> Status: Draft  
> Scope: project-specific term for HyperGraph indexing model  
> Related: `../terms-map.md`

`Derived-index` — это пересчитываемое представление состояния проекта, построенное из project files и project configuration.

`Derived-index` нужен, чтобы:
- быстро отвечать на graph queries;
- получать incoming/outgoing links без полного grep по repository;
- выполнять traversal and filtering по graph representation;
- поддерживать impact reports and affected files analysis.

В первой итерации `project-database` является `derived-index` и отражает активное состояние файлов на текущем commit/branch. При checkout другого commit или branch пользователь должен вручную пересчитать index.

`Derived-index` не является:
- authoritative Source of Truth;
- заменой Git;
- durable semantic decision сам по себе;
- невосстановимым state.
