# step-vacancy

> Status: Draft  
> Scope: project-specific term for HyperGraph methodology  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`step-vacancy` — это позиция на конкретном шаге конкретного workflow.

Она нужна, чтобы отделить:
- reusable профиль исполнителя `agent-role`;
- назначение роли на конкретный шаг процесса.

## 2. Что описывает `step-vacancy`

`step-vacancy` описывает не специалиста, а место в workflow, которое должно быть закрыто подходящей `agent-role`.

На этом уровне имеет смысл задавать:
- идентификатор позиции внутри workflow;
- ссылку на конкретный шаг workflow;
- требуемую или допустимую `agent-role`.

Важно:
- `step-vacancy` не описывает входы и выходы шага;
- `step-vacancy` не описывает, что именно нужно сделать на шаге;
- это зона ответственности самого workflow step.

Сам workflow step должен описывать:
- входы в шаг;
- что нужно сделать;
- какая `agent-role` это делает через связанную `step-vacancy`;
- какой результат должен быть получен.

## 3. Связь с `agent-role`

Связь однонаправленная:
- workflow определяет `step-vacancy`;
- `step-vacancy` ссылается на `agent-role`;
- `agent-role` не знает, где именно он будет использоваться.

Это дает гибкость:
- одна и та же роль может использоваться в разных шагах одного workflow;
- одна и та же роль может использоваться в разных workflow;
- workflow можно менять без пересборки самой роли.

## 4. Аналогия для понимания

Полезная аналогия такая:
- `agent-role` — это специалист с определенным образом мышления, skills и tools;
- `step-vacancy` — это вакансия на конкретную позицию в конкретном процессе;
- сам workflow step — это уже описание работы, которую нужно выполнить на этой позиции.

Один и тот же специалист может закрывать разные вакансии, если подходит по своему профилю.

## 5. Почему это важно

Явное введение `step-vacancy` нужно, чтобы:
- не смешивать role semantics и workflow assignment;
- не смешивать описание workflow step и назначение роли на этот шаг;
- сохранить reusable характер `agent-role`;
- сделать workflow более явным и трассируемым;
- подготовить основу для будущей formal specification workflow assignment layer.

## 6. Что не стоит смешивать с `step-vacancy`

С `step-vacancy` не стоит смешивать:
- сам reusable `agent-role`;
- конкретную `LLM model`;
- runtime projection для Kilo Code;
- role-specific `skills`, `rules` и `MCP tools` как часть core role profile.

`step-vacancy` отвечает именно за место роли в workflow, а не за reusable semantics самой роли.

## 7. Связанные термины

`step-vacancy` нужно читать вместе с:
- `agent-role`;
- `workflow`;
- `methodology workflow`;
- `Project Portable Intent`.

Этот термин является ключевым для разделения reusable role layer и workflow assignment layer.
