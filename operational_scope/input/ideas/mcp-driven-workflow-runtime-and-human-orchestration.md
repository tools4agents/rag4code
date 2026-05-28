# Idea: MCP-driven workflow runtime and human orchestration

## Контекст

Идея извлечена из [`agents_opportunities.md`](../discussion/agents_opportunities.md) как развитие уже существующих канонических положений:
- MCP является navigation and traceability interface в [`interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md);
- process model [`workflow`](../../docs/terms/project/terms/workflow.md) -> [`workflow-step`](../../docs/terms/project/terms/workflow-step.md) -> [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md) -> [`agent-role`](../../docs/terms/project/terms/agent-role.md) описан в [`workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md).

Discussion добавляет следующий слой: MCP можно рассматривать не только как lookup interface, но и как human-guided runtime control plane для исполнения methodology workflow.

## Суть идеи

MCP может стать интерфейсом, через который агент и человек работают с активным workflow execution context.

Ключевой тезис:
- source of truth по-прежнему остается file-first;
- MCP не подменяет workflow artifacts;
- MCP может давать explainable runtime context и controlled operations поверх уже существующего process model.

## Что именно полезно сохранить

### 1. Runtime context delivery

Агенту может быть полезно получать через MCP:
- текущий активный workflow;
- текущий [`workflow-step`](../../docs/terms/project/terms/workflow-step.md);
- связанную [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md);
- активную [`agent-role`](../../docs/terms/project/terms/agent-role.md) и доступные ей `rules`, `skills` и `MCP tools`;
- входы шага, `DoD`, failure criteria и expected outputs.

### 2. Human-in-the-loop orchestration

Человек может оставаться orchestrator-ом execution flow:
- выбирать, какой workflow сейчас активен;
- подтверждать переход между шагами;
- инициировать review loops;
- видеть, почему для шага активирована именно эта роль;
- запускать controlled re-materialization или binding switch для эксперимента.

### 3. Controlled write operations

Помимо navigation MCP потенциально может поддерживать controlled actions:
- отметить шаг как started / blocked / completed;
- записать handoff note;
- обновить execution status;
- запросить recompute связанного runtime context.

Это полезно только если write operations остаются explainable и не становятся теневым SoT.

## Предварительная ценность

Такая модель может дать:
- более удобное исполнение methodology workflow в mixed team `human + agent`;
- меньше необходимости вручную искать step context по нескольким файлам;
- прозрачный handoff между ролями и шагами;
- основу для future Web UI / MCP parity вокруг одного execution model.

## Примеры полезных runtime operations

Это не contract proposal, а набор candidate directions:
- получить active workflow context;
- получить данные текущего шага;
- получить resolved role context для active step;
- перечислить доступные transitions;
- отметить результат шага и причину блокировки;
- получить explainability, почему выбран именно этот role binding.

## Что важно не смешивать

С этой идеей не нужно смешивать:
- канонические authoring rules для workflow docs;
- contract policy;
- Web UI implementation detail;
- runtime-generated state как новый semantic owner layer.

## Открытые вопросы

- Где проходит граница между navigation MCP и orchestration MCP?
- Как хранить transient execution state без размывания file-first SoT?
- Нужно ли отдельное понятие active workflow session?
- Должен ли human orchestration model входить в methodology runtime canon или это отдельный interface layer?

## Статус

Идея зафиксирована как важное направление для runtime orchestration model.
Пока в каноне MCP остается прежде всего navigation interface, а orchestration semantics требуют отдельной проработки.
