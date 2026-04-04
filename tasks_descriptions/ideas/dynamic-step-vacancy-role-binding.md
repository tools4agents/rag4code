# Idea: Dynamic step-vacancy role binding

## Контекст

Идея возникла во время проектирования терминов `agent-role`, `step-vacancy`, `workflow` и `workflow-step` для `Project Methodology Runtime`.

В текущем baseline:
- `agent-role` — reusable профиль исполнителя;
- `step-vacancy` — позиция на конкретном шаге workflow;
- `workflow-step` хранит ссылку на `step-vacancy` и назначенную на нее `agent-role`.

## Суть идеи

В будущем может понадобиться отдельный конфигурационный слой, который позволит динамически переключать `agent-role` на уже существующие `step-vacancy` без переписывания самих workflow step документов.

Примеры сценариев:
- сравнить старую и новую версию одной и той же роли;
- временно заменить роль на альтернативную для эксперимента;
- переключить шаг workflow на другую роль под другой агентный runtime;
- быстро адаптировать процесс под новый reusable role pack.

## Предварительная ценность

Такой слой может дать:
- гибкое сравнение разных role profiles на одном и том же шаге;
- меньше изменений в самих workflow документах;
- более удобные эксперименты с методологией;
- лучшую адаптацию workflow под evolving agent systems;
- основу для A/B-подобного сравнения role prompts и role packs.

## Возможное направление развития

На уровне архитектуры это может оформиться как отдельный binding layer между:
- `workflow-step`;
- `step-vacancy`;
- `agent-role`.

Тогда:
- `workflow-step` описывает сам шаг;
- `step-vacancy` описывает позицию на шаге;
- binding config решает, какая конкретная роль сейчас назначена на эту позицию.

## Открытые вопросы

- Должен ли этот binding layer жить в `Project Portable Intent` или в отдельном экспериментальном overlay?
- Нужна ли история переключений role bindings?
- Должен ли binding layer поддерживать разные `primary_agent_system` или только один активный adapter target?
- Нужно ли разрешать fallback role для одной и той же `step-vacancy`?

## Статус

Идея зафиксирована как future evolution и пока не входит в текущую реализацию `Project Methodology Runtime`.