# План миграции slug на `hyper-*`

## Контекст
На этапе MVP фиксирован новый компонент `hyper-project-memory`.

Текущая стратегия (режим 2):
1. сейчас создаем и развиваем `hyper-project-memory`;
2. отдельно планируем миграцию существующих slug в `hyper-*` для консистентности бренда.

## Цель миграции
Привести slug компонентов к единому формату:
- `hyper-code-atlas`
- `hyper-code-rag`
- `hyper-project-memory`

## Scope

### In Scope
- Переименование component slug в HSM registry и связанных docs.
- Обновление ссылок в документации и планах.
- Введение backward-compatible alias на переходный период.

### Out of Scope
- Переписывание внутренней бизнес-логики сервисов.
- Изменение контрактов API только ради имен.

## Этапы

1. **Inventory**
   - собрать все упоминания `code-atlas` и `code-rag` как slug в manifests/docs/scripts.

2. **Alias Layer**
   - добавить alias mapping в HSM/registry:
     - `code-atlas -> hyper-code-atlas`
     - `code-rag -> hyper-code-rag`

3. **Primary Rename**
   - обновить канонические имена в manifests и docs.

4. **Compatibility Window**
   - оставить alias на фиксированный период.

5. **Cleanup**
   - удалить deprecated alias после стабилизации.

## Риски
- broken references в документации и CI scripts.
- drift между root и nested repo manifests.

## Mitigation
- централизованный mapping table.
- dry-run link check перед merge.
- staged rollout по репозиториям.

## Definition of Done
- все канонические ссылки используют `hyper-*` slug;
- alias слой активен и протестирован;
- migration checklist закрыт и зафиксирован.
