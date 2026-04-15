# workflow-pack

> Status: Draft  
> Scope: project-specific term for HyperGraph artifact packaging model  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`workflow-pack` — это packaging boundary для одного `workflow`.

Он нужен, чтобы хранить связанные source artifacts workflow как согласованный package, не смешивая semantic process entity и filesystem layout.

## 2. Зачем нужен этот термин

Термин нужен, чтобы отделить:
- сам `workflow` как process map;
- физическую директорию, в которой лежат artifacts этого workflow;
- support artifacts, помогающие читать и поддерживать workflow;
- runtime materialization и execution state, которые не принадлежат source pack.

Без этого distinction легко спутать:
- процесс как смысловую сущность;
- markdown-файл с обзором процесса;
- директорию со связанными файлами;
- runtime entrypoint для агента.

## 3. Что может входить в `workflow-pack`

В `workflow-pack` могут входить:
- канонический workflow overview markdown;
- navigation/readme entrypoint для людей и агентов;
- setup/install guide для подключения pack к новому проекту;
- ссылки на связанные `workflow-step`;
- workflow-level metadata;
- общие references;
- support artifacts, относящиеся ко всему workflow.

При этом сам `workflow-pack` не должен подменять отдельные `workflow-step-pack`.

## 4. Слои ответственности внутри `workflow-pack`

Чтобы `workflow-pack` оставался reusable и не смешивал разные виды смысла, его файлы должны иметь разные зоны ответственности.

### `README.md`

`README.md` внутри `workflow-pack` является navigation entrypoint.

Он отвечает на вопросы:
- что это за workflow-pack;
- как его выполнять в уже подключенном проекте;
- как его подключить в новый проект;
- куда идти дальше по pack navigation.

`README.md` не должен становиться каноническим местом для detailed process semantics, project policy или step-level logic.

### `workflow.md`

`workflow.md` является reusable process contract для всего workflow.

Он отвечает на вопросы:
- какие у workflow есть шаги;
- в каком порядке они выполняются;
- какие workflow-level invariants действуют всегда;
- какой handoff model и exchange layer нужны между шагами.

`workflow.md` должен задавать reusable semantics и не должен хардкодить project-local branch names, release units, release-note paths или другие adaptation values.

### `STEP.md` / `SKILL.md`

`STEP.md` и `SKILL.md` внутри `workflow-step-pack` отвечают за semantics конкретного шага.

Они должны описывать:
- назначение шага;
- входы, действия, ограничения и выходы шага;
- как шаг использует project-local policy и workflow-instance handoff.

Они не должны подменять собой ни весь workflow, ни project-local policy documents.

### `setup_instructions.md`

`setup_instructions.md` отвечает за adoption/install semantics.

Он должен объяснять:
- какие project-local files нужны workflow-pack;
- где они должны лежать;
- какие templates/examples использовать для интеграции.

Этот файл нужен для внедрения pack в новый проект, а не для runtime execution уже подключенного workflow.

### `terms.md`

`Workflow-pack` может иметь собственную workflow-local terms page, например `terms.md`.

Такая страница нужна, когда у workflow появляются локальные термины, которые:
- активно переиспользуются между `workflow.md` и несколькими step docs;
- не являются project-wide glossary terms;
- не должны каждый раз переопределяться прямо в focused specs шага.

Типичный пример: gate/stage terminology конкретного workflow.

Такая page не заменяет project glossary в `docs/terms/`, а задает локальный terminology contract внутри самого pack.

Если workflow-packу нужна такая страница, можно опираться на template [`workflow-local-terms.template.md`](../../../methodology-layer/assets/terms-management/resources/workflow-local-terms.template.md).

### `resources/`

`resources/` хранит support artifacts для внедрения и чтения pack:
- templates;
- examples;
- layout maps;
- вспомогательные reference materials.

`resources/` не являются runtime state и не должны подменять собой project-local context текущего проекта.

## 5. Что должно приходить извне `workflow-pack`

Чтобы reusable workflow не превращался в project-specific монолит, часть ответственности должна жить вне `workflow-pack`.

### Project-local context

Из project-local context workflow-pack должен читать:
- release policy и branch policy;
- repository boundaries;
- release units и exclusions;
- release note locations;
- Docker/release naming;
- mutable version registry;
- recovery и atomicity rules.

Эта информация должна жить в `project/`, а не дублироваться как fixed truth внутри reusable pack.

### Workflow-instance execution state

Instance-specific decisions и execution evidence должны жить в [`workflow-exchange-layer`](./workflow-exchange-layer.md), а не в source files pack.

Сюда относятся:
- текущий `release-run.md`;
- step handoff artifacts;
- branch matrix конкретного прогона;
- approved scope и exclusions конкретного прогона;
- publication evidence конкретного релиза.

## 6. Важный invariant

`Workflow-pack` является packaging boundary, но не semantic collapse.

Это значит:
- файлы workflow могут лежать рядом внутри одной директории;
- но сам `workflow`, его шаги и support artifacts остаются разными сущностями;
- physical proximity не отменяет логических границ.

Из этого же следует дополнительный layering invariant:
- navigation files не должны подменять process contract;
- reusable workflow semantics не должны подменять project-local policy;
- source pack не должен подменять workflow-instance runtime state.

## 7. Что не стоит смешивать с `workflow-pack`

С `workflow-pack` не стоит смешивать:
- сам термин `workflow`;
- `workflow-step-pack`;
- `skill` как reusable capability;
- runtime materialization state;
- execution instance конкретного прогона workflow.

Также не стоит смешивать внутри самого pack:
- navigation layer (`README.md`);
- reusable process layer (`workflow.md`);
- step semantics layer (`STEP.md`, `SKILL.md`);
- installation/adoption layer (`setup_instructions.md`);
- workflow-local terminology layer (`terms.md`), если она нужна pack;
- project-local policy layer (`project/` конкретного проекта);
- workflow-instance execution layer (`operational_scope/...` конкретного проекта).

## 8. Связанные термины

`workflow-pack` нужно читать вместе с:
- `workflow`;
- `workflow-step`;
- `workflow-step-pack`;
- `workflow-exchange-layer`;
- `skill`.

Этот термин нужен для artifact-oriented packaging model в HyperGraph.
