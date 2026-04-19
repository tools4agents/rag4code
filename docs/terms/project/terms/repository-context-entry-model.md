# repository-context-entry-model

> Status: Draft  
> Scope: project-specific term for HyperGraph project context loading model  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`Repository-context-entry-model` - это система входных точек и загрузки контекста проекта, которая задает `structure + navigation + ownership` для project-scoped agent work.

Термин нужен, чтобы явно описывать:
- какие entry-point artifacts должен иметь проект;
- в каком порядке их читать;
- какой слой чем владеет;
- как agent work входит в корректный project context без чтения всего repository подряд.

## 2. Что входит в `repository-context-entry-model`

В baseline model сюда входят:
- `AGENTS.md` как router artifact;
- `project/` как durable context layer;
- `docs/` как `Engineering Documentation SoT`;
- `operational_scope/` как execution layer;
- `.kilo/` как target `agent-system` runtime/config layer.

Эта модель отвечает не за содержимое всех этих слоев во всех деталях, а за:
- систему входных точек;
- loading order;
- ownership split между слоями.

## 3. Что это не означает

`Repository-context-entry-model` не означает:
- heuristic project discovery;
- classification `.git` roots;
- contract policy;
- process semantics workflow execution;
- adapter implementation manual.

То есть этот термин не должен смешиваться с `project-discovery`.

## 4. Связь с nested repos

`Repository-context-entry-model` включает [`nested-repo-context-switching`](nested-repo-context-switching.md) как часть loading model.

Это означает:
- parent repository задает outer navigation только до входа в nested project scope;
- autonomous nested project должен иметь право на собственный local context;
- fallback inheritance допустим только для отсутствующего слоя.

## 5. Почему это важно

Термин нужен, чтобы:
- поддерживать `lazy loading` и `progressive disclosure` для project context;
- отделить navigation contract от engineering SoT и execution artifacts;
- сделать repository context explainable для человека и агента;
- избежать drift между `AGENTS.md`, `project/`, `docs/`, `operational_scope/` и `.kilo/`.

## 6. Текущий статус в taxonomy

На текущем этапе `repository-context-entry-model` фиксируется как focused specification, а не как отдельный asset type.

Если позже появляется reusable asset packaging для этой системы, его правильный taxonomy-level тип — `project-context-entry-system asset`.

## 7. Связанные термины

`Repository-context-entry-model` нужно читать вместе с:
- `nested-repo-context-switching`;
- `manual-hybrid discovery`;
- `Engineering Documentation SoT`;
- `project-scoped runtime`.
