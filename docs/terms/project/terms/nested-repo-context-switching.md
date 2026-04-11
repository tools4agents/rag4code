# nested-repo-context-switching

> Status: Draft  
> Scope: project-specific term for HyperGraph repository context loading model  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`Nested-repo-context-switching` - это правило, по которому агент переключается с parent project context на local context автономного nested project, когда task scope уходит внутрь этого nested repository.

Термин нужен, чтобы явно отделить:
- outer repository navigation;
- выбор текущего project scope;
- загрузку local context для autonomous nested project.

## 2. Что означает `nested-repo-context-switching`

Этот термин фиксирует следующую логику:
- nested repository может иметь собственный `AGENTS.md`, `project/`, `docs/`, `operational_scope/` и `.kilo/`;
- если задача относится к этому nested repository, агент должен читать его local entry points, а не продолжать работать по parent context;
- parent repo может использоваться как outer navigation layer только до входа в локальный scope nested project.

## 3. Что это не означает

`Nested-repo-context-switching` не означает:
- что любой nested `.git` автоматически считается самостоятельным project без confirmed classification;
- что parent project теряет знание о существовании nested project;
- что локальный context nested project должен наследовать parent canon поверх своего собственного.

Discovery и classification nested roots принадлежат отдельному bounded context `project-discovery`.

## 4. Связь с repository context entry model

`Nested-repo-context-switching` является частью [`repository-context-entry-model`](repository-context-entry-model.md).

Связь такая:
- `repository-context-entry-model` задает систему входных точек и loading order;
- `nested-repo-context-switching` задает правило переключения между parent и nested local context внутри этой системы.

## 5. Связь с git boundaries

Термин нужно читать вместе с repository ownership rules.

Практически это означает:
- `project/gitContext.md` должен фиксировать autonomous nested projects и их boundaries;
- git operations должны выполняться в repository, которому принадлежат измененные файлы;
- context switching и git switching обычно совпадают, но не являются одной и той же semantic rule.

## 6. Почему это важно

Явное введение термина нужно, чтобы:
- не смешивать local canon разных repositories;
- сохранить explainable navigation для человека и агента;
- поддержать monorepo-like и nested-repo layouts без silent context drift;
- не превращать parent `AGENTS.md` в universal override для всех дочерних проектов.

## 7. Связанные термины

`Nested-repo-context-switching` нужно читать вместе с:
- `repository-context-entry-model`;
- `manual-hybrid discovery`;
- `nested-project`;
- `external-project-reference`.
