# Task: Создать `agent-role` специалиста по документации

## Контекст
- Источник: текущее развитие HyperGraph asset packs для `agent-role`, `rules` и `skills`.
- Связанные артефакты:
  - [`agent-role`](../../docs/terms/project/terms/agent-role.md)
  - [`role-pack`](../../docs/terms/project/terms/role-pack.md)
  - [`agent-system`](../../docs/terms/project/terms/agent-system.md)
  - [`agent-system-specific asset`](../../docs/terms/project/terms/agent-system-specific-asset.md)
  - [`Workflow and Roles for Project Methodology Runtime`](../../docs/methodology-layer/workflow-and-roles.md)
  - [`Artifact Model for Project Methodology Runtime`](../../docs/methodology-layer/artifact-model.md)
  - [`Naming Conventions for Project Methodology Runtime`](../../docs/methodology-layer/naming-conventions.md)
  - [`Навигация и гранулярность документации`](../../assets/rules/rules/documentation-navigation-and-granularity.md)
  - [`Ссылки на термины и их переиспользование`](../../assets/rules/rules/term-links-and-reuse.md)

## Цель
- Спроектировать reusable `agent-role` специалиста по документации для HyperGraph.
- Подготовить abstract role definition и создать Kilo-specific `agent-system` asset для этой роли.

## Scope
- Определить назначение, границы и образ мышления роли.
- Зафиксировать, какие documentation-oriented `rules`, `skills` и tools ей нужны.
- Спроектировать структуру role unit в согласии с `role-pack` model.
- Создать Kilo-specific role asset как первую concrete `agent-system` representation.

## Non-scope
- Полная materialization роли под все `agent-system`.
- Автоматическая генерация runtime artifacts.
- Поддержка других `agent-system`, кроме Kilo, на этом шаге.

## Шаги реализации
- [ ] Сформулировать purpose и boundaries documentation specialist role.
- [ ] Определить reusable responsibilities роли в терминах HyperGraph docs workflow.
- [ ] Зафиксировать required `rules`, candidate `skills` и preferred tools.
- [ ] Подготовить abstract role artifact structure для pack layout.
- [ ] Создать Kilo-specific role asset, согласованный с abstract role semantics.

## Definition of Done
- [ ] Есть согласованное описание новой documentation specialist role.
- [ ] Есть понимание ее места в reusable `agent-role` pack model.
- [ ] Есть список связных `rules` и candidate `skills`.
- [ ] Есть Kilo-specific `agent-system` asset для этой роли.

## Execution Status
- Current State: Задача поставлена; роль еще не спроектирована.
- Next Step: Подготовить short design для abstract role semantics, а затем на его основе собрать Kilo-specific role asset.
- Blockers: none
- Contract Changes: none
- Verification: Проверить согласованность роли с [`agent-role`](../../docs/terms/project/terms/agent-role.md), [`role-pack`](../../docs/terms/project/terms/role-pack.md), Kilo-specific representation model и documentation rules.
