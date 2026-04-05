# Plan: Нормализация `agent-role` discussion в каноническую документацию

## Контекст
- Источник обсуждения: `operational_scope/discussion/agent-role-discussion.md`
- Уже зафиксированные связанные артефакты:
  - `docs/terms/project/terms/agent-role.md`
  - `docs/terms/project/terms/step-vacancy.md`
  - `docs/terms/project/terms/workflow.md`
  - `docs/terms/project/terms/workflow-step.md`
  - `docs/adr/0002-separate-artifacts-for-agent-role-and-kilocode-projection.md`
  - `docs/methodology-layer/workflow-and-roles.md`

## Цель
Перевести накопленную discussion-спецификацию по `agent-role` из временного обсуждения в набор канонических focused docs слоя `Project Methodology Runtime`, чтобы `operational_scope/discussion/agent-role-discussion.md` перестал быть единственным носителем ключевых решений.

## Проблема
Сейчас важные решения по:
- portable core `agent-role`
- KiloCode projection
- `when_to_use`
- `file_access_policy`
- `primary_agent_system`
- role packs
- связи `workflow -> step-vacancy -> agent-role`

сосредоточены в discussion-документе. Это полезно для этапа обсуждения, но неудобно как долгосрочный Source of Truth.

## Целевое состояние
После выполнения плана:
- ключевые решения из `operational_scope/discussion/agent-role-discussion.md` разложены по каноническим focused specs;
- discussion-doc либо удаляется как временный buffer artifact, либо удаляется после короткого финального прохода по остаточным деталям;
- термины, architectural decisions и focused specs больше не расходятся между собой;
- `agent-role` описан как reusable сущность, а adapter projection — как отдельный artifact layer.

## Предлагаемая карта переноса

### 1. В `docs/methodology-layer/artifact-model.md`
Перенести:
- место `agent-role` в meta-model;
- место role packs как packaging convention на уровне artifacts;
- связь core role artifact и adapter projection artifact;
- место `workflow`, `workflow-step` и `step-vacancy` как artifact families.

### 2. В `docs/methodology-layer/workflow-and-roles.md`
Перенести:
- каноническую модель `agent-role`;
- distinction между role, `step-vacancy`, `workflow-step` и `workflow`;
- однонаправленную связь `workflow -> step-vacancy -> agent-role`;
- `when_to_use` как explainability hint роли;
- reusable role packs и связь role с process layer.

### 3. В `docs/methodology-layer/interfaces-and-storage.md`
Перенести:
- четыре состояния хранения для role artifacts и adapter projection;
- `primary_agent_system` как project-level selector;
- resolved runtime representation;
- границу между core artifact, adapter projection и materialized runtime.

### 4. В `docs/contracts/`
Позже отразить:
- contract-level schemas для role pack и adapter projection;
- links на formal contracts, когда они появятся.

## Что должно остаться в discussion doc
Целевая модель для `operational_scope/discussion/agent-role-discussion.md` изменилась.

Так как `docs/specification/` должен содержать только SoT спецификации, discussion doc после нормализации не должен сохраняться как постоянный artifact и должен жить в `operational_scope/discussion/` до завершения работы.

Допустимы только два варианта:
- либо выполнить короткий финальный проход по остаточным деталям и затем удалить файл;
- либо, если обнаружится действительно ценное неканонизированное reasoning, вынести его в ADR или RFC-like document и после этого удалить discussion file.

## Важные инварианты
При переносе нельзя потерять следующие решения:
- `agent-role` не равен конкретной `LLM model`;
- `agent-role` — reusable role profile;
- `step-vacancy` отвечает только за назначение роли на шаг;
- `workflow-step` отвечает за подробное описание работы шага;
- `when_to_use` полезен как role hint, но не заменяет workflow assignment;
- `customInstructions` трактуется как optional overlay;
- `roleDefinition` трактуется как KiloCode-specific rendered field;
- core role и KiloCode projection остаются separate artifacts по `ADR 0002`.

## Риски
- часть discussion-материала может быть случайно потеряна при переносе;
- возможны новые дубли между `artifact-model.md`, `workflow-and-roles.md` и `interfaces-and-storage.md`;
- если не зафиксировать четкие границы ответственности файлов, discussion просто переедет в другое место без реальной нормализации.

## Следующий шаг
После утверждения этого плана нужно:
1. Создать канонический `docs/methodology-layer/workflow-and-roles.md`.
2. Перенести в него process и role model.
3. Обновить `artifact-model.md` и `interfaces-and-storage.md`.
4. Выполнить короткий финальный проход по остаточным деталям `operational_scope/discussion/agent-role-discussion.md`.
5. После переноса или ADR-extraction удалить `operational_scope/discussion/agent-role-discussion.md` как временный buffer artifact.

## Ожидаемый результат
`agent-role` discussion перестает быть временным knowledge island и становится частью стабильной канонической документации слоя.
