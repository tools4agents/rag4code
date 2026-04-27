# workflow

> Status: Draft  
> Scope: project-specific term for HyperGraph methodology  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`workflow` — это semantic process entity, которая описывает markdown-defined directed graph for agent execution, объединенный общей целью и общим смыслом.

Он нужен, чтобы зафиксировать:
- для чего существует процесс;
- какие вершины и переходы в него входят;
- как человек и агент проходят от начала процесса к результату.

`workflow` может быть:
- частью общей методологии проекта;
- локальным процессом для отдельного класса задач;
- reusable process pattern, который можно применять повторно.

Короткая практическая формула:

```text
workflow = markdown-defined directed graph for agent execution
```

То есть workflow является human-readable и agent-readable описанием process graph, а не только prose-инструкцией.

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
- `workflow-step-gate` как specialized `workflow-step` для explicit readiness / eligibility / routing decision;
- nested `workflow` как вложенный process graph, который сам раскрывается в собственную карту шагов или под-workflow;
- user interaction node как external human interaction point;
- lifecycle marker как вход/выход workflow-run.

Проект или конкретный workflow-pack может ввести и другие vertex classes, если они не размывают semantic границы процесса.

Важно:
- не каждая вершина workflow обязана быть `workflow-step`;
- если вершина сама содержит несколько переходов, gate-steps, optional branches или conditional loops, ее нужно моделировать как nested `workflow`, а не как перегруженный `workflow-step`;
- если вершина принимает explicit readiness / eligibility / routing decision, ее нужно моделировать как [`workflow-step-gate`](./workflow-step-gate.md), даже если gate-step остается lightweight.

## 2.2 Nested workflows

`Workflow` может содержать другие `workflow` как вершины своего process graph.

Это нужно, когда верхнеуровневый процесс состоит из крупных стадий, каждая из которых сама имеет внутреннюю последовательность шагов, gate-steps, exception paths или conditional subflows.

Пример semantic hierarchy:

```text
SDLC workflow
  -> stage workflow
      -> workflow-step
```

Или более общий случай:

```text
workflow
  -> workflow-step
  -> nested workflow
      -> workflow-step
      -> nested workflow
```

Правило выбора:

- если vertex можно выполнить как bounded atomic execution unit, materialize it as `workflow-step`;
- если vertex требует собственной карты процесса, transition semantics и нескольких execution units, materialize it as nested `workflow`;
- один агент может выполнить несколько последовательных `workflow-step`, но это не превращает их в один semantic step.

## 2.3 Как workflow обычно materialize-ится в документации

Каноническое описание workflow часто включает:
- graph overview diagram;
- vertex table;
- edge / transition table;
- happy path vs exception/remediation path separation.

Это не обязательно всегда, но для non-linear workflow такая форма становится preferred baseline.

## 2.4 Полезные аналогии

Для понимания `workflow` полезны две аналогии.

### LangGraph analogy

`workflow` похож на markdown-based LangGraph graph:

- vertices задают `workflow-step`, `workflow-step-gate`, nested `workflow`, human interaction или lifecycle marker;
- edges задают transitions, handoff rules и условия перехода;
- nested workflows похожи на вложенные graph/subgraph;
- workflow-instance state живет не в source pack, а в operational layer конкретного прогона.

Подробно см. [`langgraph-analogy.md`](./resources/workflow/langgraph-analogy.md).

### C4 analogy

`workflow` также похож на C4-style progressive disclosure:

- верхний workflow показывает общий process context;
- nested workflow раскрывает крупную стадию;
- `workflow-step` раскрывает bounded execution unit;
- skill или runtime command materialization находится еще ниже и не подменяет process map.

Подробно см. [`c4-analogy.md`](./resources/workflow/c4-analogy.md).

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
- ссылки на nested `workflow` и их `workflow-pack`, если workflow декомпозируется на под-workflow;
- workflow-level metadata;
- общие workflow-level references и support artifacts.

Это позволяет хранить process map отдельно от support materials, не превращая один markdown в перегруженный монолит.

## 5. Связь с `workflow-step` и nested `workflow`

`Workflow` — это карта процесса или process graph.

Каждая исполняемая atomic step-вершина в этой карте должна ссылаться на отдельный `workflow-step`, который раскрывает шаг подробно.

Если вершина является не atomic step, а внутренним процессом, она должна ссылаться на nested `workflow`.

То есть:
- `workflow` дает обзорную карту процесса;
- `workflow-step` дает глубокое описание конкретного шага;
- `workflow-step-gate` дает глубокое описание gate-step, verdicts и routing decision;
- nested `workflow` дает карту внутреннего процесса для крупной стадии или subflow;
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
- `workflow-step-gate`;
- `workflow-step-pack`;
- `workflow-exchange layer`;
- `step-vacancy`;
- `agent-role`;
- [`Operational Documentation Layer`](./operational-documentation-layer.md).

Adjacent resources:

- [`langgraph-analogy.md`](./resources/workflow/langgraph-analogy.md);
- [`c4-analogy.md`](./resources/workflow/c4-analogy.md).

Этот термин является ключевым для понимания process layer в `Project Methodology Runtime`.
