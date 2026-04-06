# Task: Создать skill для проверки правил документации

## Контекст
- Источник: введены новые documentation rules для заголовков, терминов, ссылок и гранулярности.
- Связанные артефакты:
  - [`skill-doc`](../../docs/methodology-layer/artifact-model.md)
  - [`Навигация и гранулярность документации`](../../assets/rules/rules/documentation-navigation-and-granularity.md)
  - [`Ссылки на термины и их переиспользование`](../../assets/rules/rules/term-links-and-reuse.md)
  - [`Заголовки документации`](../../assets/rules/rules/documentation-headings.md)
  - [`agent-role`](../../docs/terms/project/terms/agent-role.md)

## Цель
- Спроектировать специализированный skill для проверки документации на соответствие новым documentation rules.
- Сделать его пригодным для использования documentation specialist role и других quality-oriented roles.

## Scope
- Определить trigger conditions и expected inputs skill.
- Зафиксировать checklist проверки documentation rules.
- Определить expected output format для findings и remediation hints.

## Non-scope
- Автоматическая правка всей документации.
- Полный lint engine или code implementation.

## Шаги реализации
- [ ] Определить назначение и границы skill.
- [ ] Зафиксировать набор проверяемых documentation rules.
- [ ] Спроектировать expected workflow входов, шагов анализа и output format.
- [ ] Определить, как skill будет сочетаться с documentation specialist role.
- [ ] Подготовить draft skill artifact.

## Definition of Done
- [ ] Есть согласованный scope skill.
- [ ] Есть checklist проверок по documentation rules.
- [ ] Есть структура output findings.
- [ ] Есть понимание связи skill с documentation specialist role.

## Execution Status
- Current State: Задача поставлена; skill еще не спроектирован.
- Next Step: Выделить минимальный reusable protocol проверки documentation rules.
- Blockers: none
- Contract Changes: none
- Verification: Проверить, что skill опирается на актуальные rules и не дублирует glossary или methodology semantics без необходимости.
