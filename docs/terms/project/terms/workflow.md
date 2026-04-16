# workflow

> Status: Draft  
> Scope: project-specific term for HyperGraph methodology  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`workflow` — это semantic process entity, которая описывает направленный process graph, объединенный общей целью и общим смыслом.

Он нужен, чтобы зафиксировать:
- для чего существует процесс;
- какие вершины и переходы в него входят;
- как человек и агент проходят от начала процесса к результату.

`workflow` может быть:
- частью общей методологии проекта;
- локальным процессом для отдельного класса задач;
- reusable process pattern, который можно применять повторно.

## 2. Что описывает `workflow`

На semantic layer `workflow` описывает:
- цель workflow и зачем он нужен;
- directed process graph;
- вершины workflow и их роли;
- переходы между вершинами и условия этих переходов;
- high-level navigation по процессу;
- optional общие входы и выходы workflow;
- happy path и exception/remediation paths;
- optional high-level transition notes между вершинами.

Минимально workflow должен описывать:
- для чего он нужен;
- directed graph процесса или его эквивалентную карту переходов.

Линейная последовательность шагов — это частный случай workflow, а не его единственная возможная форма.

## 2.1 Типы вершин внутри `workflow`

В workflow могут встречаться разные типы вершин.

Базово допустимы:
- `workflow-step` как исполняемая единица работы;
- user interaction node как external human interaction point;
- lifecycle marker как вход/выход workflow-run.

Проект или конкретный workflow-pack может ввести и другие vertex classes, если они не размывают semantic границы процесса.

Важно:
- не каждая вершина workflow обязана быть `workflow-step`;
- но если gate имеет собственные входы, выходы, handoff и самостоятельную execution ценность, он может materialize-иться как отдельный `workflow-step`.

## 2.2 Как workflow обычно materialize-ится в документации

Каноническое описание workflow часто включает:
- graph overview diagram;
- vertex table;
- edge / transition table;
- happy path vs exception/remediation path separation.

Это не обязательно всегда, но для non-linear workflow такая форма становится preferred baseline.

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

`Workflow` — это карта процесса или process graph.

Каждый шаг в этой карте должен ссылаться на отдельный `workflow-step`, который раскрывает шаг подробно.

То есть:
- `workflow` дает обзорную карту процесса;
- `workflow-step` дает глубокое описание конкретного шага;
- агент обычно исполняет не весь workflow одним запросом, а выбранный `workflow-step` или другой explicit execution node.

Такой подход поддерживает `lazy loading` и `progressive disclosure`.

## 5.1 Связь с [`workflow-exchange layer`](./workflow-exchange-layer.md)

В document-driven lifecycle знание и handoff workflow не обязаны жить только внутри канонического workflow-pack.

Если workflow исполняется как реальный multi-step directed process graph, у него может быть свой [`workflow-exchange layer`](./workflow-exchange-layer.md) внутри [`Operational Documentation Layer`](./operational-documentation-layer.md).

Это означает:

- `workflow` как semantic process entity может иметь временный operational layer для конкретных прогонов;
- такой слой может хранить instance-specific handoff artifacts, graph-state и transition evidence между шагами workflow;
- этот слой не является [`Engineering Documentation SoT`](./engineering-documentation-sot.md);
- этот слой не является [`Release Documentation Layer`](./release-documentation-layer.md);
- после завершения конкретного workflow-run эти artifacts могут быть удалены.

Важно различать:

- `workflow` как process map;
- `workflow-pack` как source packaging boundary;
- [`workflow-exchange layer`](./workflow-exchange-layer.md) как временный operational exchange layer для конкретного прогона.

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
- перечислить вершины процесса;
- показать переходы и их условия;
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
- поддерживать non-linear directed process graphs, а не только линейные цепочки;
- сделать документацию процесса удобной и для человека, и для агента;
- поддерживать reusable process patterns в проекте.

## 9. Что не стоит смешивать с `workflow`

С `workflow` не стоит смешивать:
- reusable semantics `agent-role`;
- подробное описание одного конкретного шага;
- `workflow-pack` как packaging boundary;
- [`workflow-exchange layer`](./workflow-exchange-layer.md) как временный operational exchange contour;
- runtime projection роли или шага;
- storage layout adapter artifacts.

`Workflow` — это описание процесса, а не описание packaging unit, temporary execution layer или runtime representation.

## 10. Связанные термины

`workflow` нужно читать вместе с:
- `methodology workflow`;
- `workflow-pack`;
- `workflow-step`;
- `workflow-step-pack`;
- `workflow-exchange layer`;
- `step-vacancy`;
- `agent-role`;
- [`Operational Documentation Layer`](./operational-documentation-layer.md).

Этот термин является ключевым для понимания process layer в `Project Methodology Runtime`.
