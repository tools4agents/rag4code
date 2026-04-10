# workflow-step

> Status: Draft  
> Scope: project-specific term for HyperGraph methodology  
> Related: `docs/terms/project/terms_map.md`

## 1. Назначение термина

`workflow-step` — это semantic process entity, которая подробно описывает один конкретный шаг workflow.

Он нужен, чтобы отделить:
- краткую карту всего workflow;
- детальное описание отдельного шага;
- назначение роли на шаг через `step-vacancy`;
- reusable semantics роли через `agent-role`;
- packaging boundary шага через `workflow-step-pack`.

## 2. Связь с `workflow`

`Workflow` — это верхнеуровневая process map, которая описывает:
- цель workflow и зачем он нужен;
- последовательность шагов;
- optional общие входы и выходы;
- high-level navigation по процессу.

Каждый шаг в таком workflow должен ссылаться на отдельный `workflow-step`, который и раскрывает шаг подробно.

То есть:
- `workflow` дает карту процесса;
- `workflow-step` раскрывает конкретный шаг;
- агенту обычно назначают выполнение выбранного `workflow-step`, а не всего workflow целиком.

## 3. Что описывает `workflow-step`

`Workflow-step` должен описывать:
- входы для шага;
- что нужно сделать на шаге;
- `step-vacancy` и назначенную на нее `agent-role`;
- выходы из шага;
- `DoD` шага;
- критерии провала шага с необходимостью возврата к одному из предыдущих шагов;
- связи с reusable `skills`, если шаг опирается на них.

## 4. `workflow-step` не равен pack

Важно жестко различать:
- `workflow-step` как semantic step entity;
- `workflow-step-pack` как packaging boundary для authoring и хранения artifacts этого шага.

Иными словами:
- `workflow-step` отвечает на вопрос, что именно нужно сделать на этом месте процесса;
- `workflow-step-pack` отвечает на вопрос, как source artifacts шага собраны на filesystem.

Packaging boundary не должна подменять semantic boundary.

## 5. Техническая реализация через `workflow-step-pack`

Обычно `workflow-step` authoring-ся через `workflow-step-pack`.

`Workflow-step-pack` — это директория, внутри которой могут лежать:
- канонический markdown-файл с описанием шага;
- шаблоны и чеклисты;
- examples;
- references и дополнительные описания;
- support artifacts, нужные для качественного выполнения шага.

Это делает шаг не просто prose-описанием, а executable methodology unit для человека и агента.

## 6. Связь с `skill`

`Workflow-step` может использовать reusable `skills`, но не должен отождествляться с ними.

Разделение такое:
- `skill` отвечает на вопрос, какое действие или capability можно переиспользовать в разных местах;
- `workflow-step` отвечает на вопрос, что именно нужно сделать сейчас в конкретной точке процесса;
- `workflow-step-pack` может содержать ссылки на skills, templates и локальные материалы, нужные для исполнения шага.

Таким образом шаг может быть похож на skill по форме упаковки, но не по semantic роли.

## 7. Связь с `step-vacancy`

`Workflow-step` и `step-vacancy` — это разные сущности.

- `workflow-step` описывает саму работу шага;
- `step-vacancy` описывает позицию внутри этого шага, которую должна закрыть подходящая `agent-role`.

Это позволяет не смешивать:
- описание работы;
- назначение исполнителя;
- reusable профиль исполнителя.

## 8. Связь с `agent-role`

`Workflow-step` не должен напрямую описывать reusable semantics роли.

Он должен только ссылаться на:
- `step-vacancy`;
- а через нее — на `agent-role`, которая подходит для исполнения шага.

Таким образом сохраняется разделение:
- `agent-role` — reusable профиль;
- `step-vacancy` — assignment layer;
- `workflow-step` — подробное описание работы шага.

## 9. Исполнимость шага

`Workflow-step` является нормальной execution unit для methodology workflow.

Это означает:
- агенту можно указывать выполнить конкретный шаг;
- один и тот же агент может последовательно выполнить несколько шагов, если process policy это допускает;
- но сам workflow не должен рассматриваться как одна непрозрачная инструкция для одиночного исполнения целиком.

## 10. Почему это важно

Явное описание `workflow-step` нужно, чтобы:
- workflow оставался компактной картой;
- человек и агент могли читать процесс по progressive disclosure;
- шаг можно было обсуждать, проверять и улучшать независимо от остальных шагов;
- `DoD` и критерии возврата были зафиксированы прямо на уровне шага;
- было проще строить traceability между workflow, step, vacancy, role и результатами;
- packaging шага не разрушал его semantic границы.

## 11. Минимальная структура `workflow-step`

Минимально `workflow-step` должен описывать:
- входы шага;
- действие шага;
- связанную `step-vacancy` и `agent-role`;
- выходы шага;
- `DoD` шага;
- критерии провала и условия возврата на предыдущие шаги.

## 12. Что не стоит смешивать с `workflow-step`

С `workflow-step` не стоит смешивать:
- сам reusable `agent-role`;
- конкретный `skill`;
- `workflow-step-pack` как packaging boundary;
- runtime projection для agent system;
- execution state конкретного запуска.

## 13. Связанные термины

`workflow-step` нужно читать вместе с:
- `workflow`;
- `workflow-pack`;
- `workflow-step-pack`;
- `methodology workflow`;
- `step-vacancy`;
- `agent-role`;
- `skill`.

Этот термин является ключевым для отделения карты процесса от подробного и исполнимого описания каждого шага.
