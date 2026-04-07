# Idea: Dynamic step-vacancy role binding

## Контекст

Идея возникла во время проектирования терминов [`agent-role`](../../docs/terms/project/terms/agent-role.md), [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md), [`workflow`](../../docs/terms/project/terms/workflow.md) и [`workflow-step`](../../docs/terms/project/terms/workflow-step.md) для `Project Methodology Runtime`.

В текущем baseline:
- [`agent-role`](../../docs/terms/project/terms/agent-role.md) — reusable профиль исполнителя;
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md) — позиция на конкретном шаге workflow;
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md) хранит ссылку на [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md);
- assignment layer остается однонаправленным: [`workflow`](../../docs/terms/project/terms/workflow.md) -> [`workflow-step`](../../docs/terms/project/terms/workflow-step.md) -> [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md) -> [`agent-role`](../../docs/terms/project/terms/agent-role.md).

## Суть идеи

В будущем может понадобиться отдельный конфигурационный слой, который позволит динамически переключать `agent-role` на уже существующие `step-vacancy` без переписывания самих workflow step документов.

Примеры сценариев:
- сравнить старую и новую версию одной и той же роли;
- временно заменить роль на альтернативную для эксперимента;
- переключить шаг workflow на другую роль под другой агентный runtime;
- быстро адаптировать процесс под новый reusable role pack.

## Capability-oriented extension

Во время extraction pass из [`agents_opportunities.md`](../discussion/agents_opportunities.md) стало видно, что полезно сохранить еще одно possible evolution direction.

В будущем binding layer может стать не только direct role remapping, но и capability-oriented selection layer.

В такой модели:
- `workflow-step` по-прежнему описывает работу шага;
- `step-vacancy` по-прежнему описывает позицию на шаге;
- шаг или vacancy могут дополнительно требовать capability profile;
- binding config выбирает `agent-role`, который удовлетворяет required capability set.

Это может быть полезно, если одна и та же вакансия может закрываться:
- разными версиями одной роли;
- альтернативными ролями с сопоставимыми возможностями;
- разными ролями под разные [`agent-system`](../../docs/terms/project/terms/agent-system.md).

## Предварительная ценность

Такой слой может дать:
- гибкое сравнение разных role profiles на одном и том же шаге;
- меньше изменений в самих workflow документах;
- более удобные эксперименты с методологией;
- лучшую адаптацию workflow под evolving agent systems;
- основу для A/B-подобного сравнения role prompts и role packs.

Capability-oriented extension дополнительно может дать:
- менее хрупкую привязку шага к одной конкретной роли;
- более explainable подбор роли через required capabilities;
- основу для future compatibility checks между workflow demands и available role packs.

## Возможное направление развития

На уровне архитектуры это может оформиться как отдельный binding layer между:
- `workflow-step`;
- `step-vacancy`;
- `agent-role`.

Тогда:
- `workflow-step` описывает сам шаг;
- `step-vacancy` описывает позицию на шаге;
- binding config решает, какая конкретная роль сейчас назначена на эту позицию.

Более сильный future variant:
- `workflow-step` и/или `step-vacancy` описывают required capabilities;
- binding config сопоставляет capability profile с доступными `agent-role`;
- final selected role зависит от project context, available packs и active [`primary-agent-system`](../../docs/terms/project/terms/primary-agent-system.md).

## Открытые вопросы

- Должен ли этот binding layer жить в `Project Portable Intent` или в отдельном экспериментальном overlay?
- Нужна ли история переключений role bindings?
- Должен ли binding layer поддерживать разные `primary_agent_system` или только один активный adapter target?
- Нужно ли разрешать fallback role для одной и той же `step-vacancy`?
- Должен ли capability profile быть частью `step-vacancy`, `workflow-step` или отдельного reusable artifact?
- Нужен ли distinct термин для capability-oriented binding layer, чтобы не смешивать его с current direct assignment model?

## Статус

Идея зафиксирована как future evolution и пока не входит в текущую реализацию `Project Methodology Runtime`.
