# workflow

> Status: Draft  
> Scope: project-specific term for HyperGraph methodology  
> Related: `docs/terms/project/terms_map.md`

## 1. Назначение термина

`workflow` — это semantic process entity, которая описывает последовательность шагов, объединенных общей целью и общим смыслом.

Он нужен, чтобы зафиксировать:
- для чего существует процесс;
- какие `workflow-step` в него входят;
- в каком порядке они обычно выполняются;
- как человек и агент проходят от начала процесса к результату.

`workflow` может быть:
- частью общей методологии проекта;
- локальным процессом для отдельного класса задач;
- reusable process pattern, который можно применять повторно.

## 2. Что описывает `workflow`

На semantic layer `workflow` описывает:
- цель workflow и зачем он нужен;
- последовательность шагов;
- high-level navigation по процессу;
- optional общие входы и выходы workflow;
- возможные high-level transition notes между шагами.

Минимально workflow должен описывать:
- для чего он нужен;
- последовательность шагов.

## 3. `workflow` не равен pack

Важно жестко различать:

- `workflow` как semantic process entity;
- `workflow-pack` как packaging boundary для authoring и хранения artifacts этого workflow.

Иными словами:
- `workflow` отвечает на вопрос, какой процесс существует;
- `workflow-pack` отвечает на вопрос, как связанные с этим процессом source artifacts собраны на filesystem.

Packaging boundary не должна подменять semantic boundary.

## 4. Техническая реализация через `workflow-pack`

Обычно `workflow` authoring-ся через `workflow-pack`.

`Workflow-pack` — это директория, внутри которой может лежать:
- канонический markdown-файл с описанием workflow;
- ссылки на связанные `workflow-step`;
- workflow-level metadata;
- общие workflow-level references и support artifacts.

Это позволяет хранить process map отдельно от support materials, не превращая один markdown в перегруженный монолит.

## 5. Связь с `workflow-step`

`Workflow` — это карта процесса.

Каждый шаг в этой карте должен ссылаться на отдельный `workflow-step`, который раскрывает шаг подробно.

То есть:
- `workflow` дает обзорную карту процесса;
- `workflow-step` дает глубокое описание конкретного шага;
- агент обычно исполняет не весь workflow одним запросом, а выбранный `workflow-step`.

Такой подход поддерживает `lazy loading` и `progressive disclosure`.

## 6. Связь с `methodology workflow`

`Methodology workflow` — это частный, центральный для проекта workflow.

Он отличается тем, что:
- задает основную методологию разработки проекта;
- является главным процессом, на который ориентируются разработчики и агенты;
- определяет, как связываются шаги, роли, handoff и результаты разработки.

При этом не каждый `workflow` обязан быть `methodology workflow`.

В проекте могут существовать и другие workflow:
- document consolidation workflow;
- architect review workflow;
- task handoff workflow;
- исследовательский workflow.

## 7. Связь с `step-vacancy` и `agent-role`

На уровне самого `workflow` обычно не нужно подробно раскрывать reusable semantics роли.

`Workflow` должен:
- перечислить шаги;
- показать их порядок;
- при необходимости указывать, что шаг имеет связанную `step-vacancy`.

Детали того:
- какая роль нужна шагу;
- что делает шаг;
- какие у него входы и выходы;
- какие критерии завершения и провала,

уже должны подробно раскрываться в `workflow-step`.

## 8. Почему это важно

Явное введение `workflow` как semantic entity нужно, чтобы:
- не превращать процесс в набор несвязанных step-папок без общей карты;
- отделить обзор процесса от подробностей каждого шага;
- сделать документацию процесса удобной и для человека, и для агента;
- поддерживать reusable process patterns в проекте.

## 9. Что не стоит смешивать с `workflow`

С `workflow` не стоит смешивать:
- reusable semantics `agent-role`;
- подробное описание одного конкретного шага;
- `workflow-pack` как packaging boundary;
- runtime projection роли или шага;
- storage layout adapter artifacts.

`Workflow` — это описание процесса, а не описание packaging unit или runtime representation.

## 10. Связанные термины

`workflow` нужно читать вместе с:
- `methodology workflow`;
- `workflow-pack`;
- `workflow-step`;
- `workflow-step-pack`;
- `step-vacancy`;
- `agent-role`.

Этот термин является ключевым для понимания process layer в `Project Methodology Runtime`.
