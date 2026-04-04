# Task: Пройти полный Architect Stage для Project Methodology Runtime

## Контекст
- Источник: текущее архитектурное проектирование первого базового компонента HyperGraph для project methodology management.
- Связанные артефакты:
  - [`docs/methodology-layer/overview.md`](../../docs/methodology-layer/overview.md)
  - [`docs/methodology-layer/artifact-model.md`](../../docs/methodology-layer/artifact-model.md)
  - [`docs/methodology-layer/workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md)
  - [`docs/methodology-layer/interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md)
  - [`docs/methodology-layer/project-discovery.md`](../../docs/methodology-layer/project-discovery.md)
  - [`docs/idea/project-first-model-and-storage.md`](../../docs/idea/project-first-model-and-storage.md)
  - [`docs/idea/HyperGraph_vision.md`](../../docs/idea/HyperGraph_vision.md)
  - [`docs/idea/integrated_knowledge_graph_schema.md`](../../docs/idea/integrated_knowledge_graph_schema.md)
  - [`../../../../.kilocode/skills-architect/architect-stage/SKILL.md`](../../../../.kilocode/skills-architect/architect-stage/SKILL.md)

## Architecture Context References
- [ ] [`docs/idea/project-first-model-and-storage.md`](../../docs/idea/project-first-model-and-storage.md)
- [ ] [`docs/idea/HyperGraph_vision.md`](../../docs/idea/HyperGraph_vision.md)
- [ ] [`docs/adr/0001-arcadedb-as-unified-storage-for-mvp.md`](../../docs/adr/0001-arcadedb-as-unified-storage-for-mvp.md)

## Specification References
- [ ] [`docs/methodology-layer/overview.md`](../../docs/methodology-layer/overview.md)
- [ ] [`docs/methodology-layer/artifact-model.md`](../../docs/methodology-layer/artifact-model.md)
- [ ] [`docs/methodology-layer/workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md)
- [ ] [`docs/methodology-layer/interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md)
- [ ] [`docs/methodology-layer/project-discovery.md`](../../docs/methodology-layer/project-discovery.md)

## Test Design References
- [ ] Создать или обновить отдельный Test Design artifact для этого компонента
- [ ] Обеспечить трассировку requirement -> suite -> script для критичных требований согласно [`../../../../.kilocode/skills-architect/architect-stage/SKILL.md`](../../../../.kilocode/skills-architect/architect-stage/SKILL.md)

## Workflow References
- [ ] `none`
- [ ] При необходимости в ходе работы создать отдельный workflow artifact и затем обновить эту секцию

## Цель
- Пройти все этапы Architect Stage для `Project Methodology Runtime` и спроектировать систему целиком до состояния, пригодного к последующей реализации без догадок.
- Получить полный набор архитектурных артефактов: discovery outputs, spec, domain model, diagrams, contracts, test design, ADR и review-ready package.

## Ключевой контекст для продолжения
- Речь идет о первом базовом компоненте HyperGraph, который управляет methodology assets проекта и предоставляет доступ через MCP и Web UI.
- Консолидация planning-пакета уже переведена в канонический SoT слой через [`docs/methodology-layer/artifact-model.md`](../../docs/methodology-layer/artifact-model.md), [`docs/methodology-layer/workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md), [`docs/methodology-layer/interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md) и [`docs/methodology-layer/project-discovery.md`](../../docs/methodology-layer/project-discovery.md).
- Пользователь хочет не частичный sketch, а полную Architect-stage проработку системы, готовой к воплощению.
- Пользователь отдельно попросил использовать знания о том, что описания architect skills находятся в [`/home/anton-admin/.kilocode/skills-architect`](../../../../.kilocode/skills-architect/architect-stage/SKILL.md).
- Важные уже согласованные решения, которые нельзя потерять:
  - Source of Truth для methodology artifacts — markdown и yaml files.
  - `Central methodology catalog` живет во внутреннем storage сервиса, а не в project metadata.
  - Project metadata должна быть portable и не содержать machine-specific absolute paths.
  - Runtime для agent systems materialize как единый project-scoped слой.
  - Домен строится вокруг `MethodologyArtifact` и `MethodologyArtifactType`.
  - Baseline types: `methodology-doc`, `rule-doc`, `skill-doc`, `agent-role`.
  - `agent-role` — общая сущность; для Kilo Code частным случаем является `mode`.
  - Web UI первой итерации — graph-and-config first, не markdown editor.
  - MCP первой итерации — traceability and navigation first.
  - `Project Discovery` первой итерации — manual-hybrid: сервис находит candidates, разработчик классифицирует, автоматического rediscovery нет.
  - В graph первого MVP для проектов пока нужны только вершины `Project` и связи `USES_PROJECT`, `PARENT_OF`, плюс флаг `has_local_db`.
  - `external-project-reference` — внешний проект для интеграции и анализа, не обязательно локально индексируемый как редактируемый проект.

## Ожидаемый Architect Stage scope
- Discovery требований, ограничений, NFR и open questions.
- Единый spec document как закон реализации.
- Полный domain model и invariants.
- Диаграммы архитектуры и потоков данных.
- Contract-first описание MCP, Web UI и service-core boundaries.
- Test design и coverage matrix.
- ADR для ключевых решений.
- Подготовка пакета к review gate.

## Buffer handoff после консолидации focused specs

После миграции legacy planning package в канонический слой `docs/methodology-layer/` в buffer task для полного Architect Stage нужно явно забрать те блоки, которые не входили в минимальный SoT focused spec package.

К ним относятся:
- lifecycle для `drift detection`, `indexing` и `reconcile` из legacy architecture draft;
- data flow overview и более широкая component framing для полного architect package;
- open questions, связанные с full architect stage, а не с focused spec migration;
- follow-up на domain model, contracts, test design и diagrams, которые должны попасть уже в implementation-ready architect artifacts, а не в focused spec baseline.

Эти блоки считаются не потерянными, а переназначенными в следующий buffer stage через этот task file.

## Подсказка по маршрутизации Architect Stage
Согласно [`../../../../.kilocode/skills-architect/architect-stage/SKILL.md`](../../../../.kilocode/skills-architect/architect-stage/SKILL.md), задачу нужно провести через следующие подэтапы:
- `architect-discovery`
- `architect-spec-writer`
- `architect-domain-modeler`
- `architect-diagrammer`
- `architect-contract-first`
- `architect-test-designer`
- `architect-adr-writer`
- `architect-stage-review`

## Шаги реализации
- [ ] Выполнить onboarding по Architect Stage references и зафиксировать scope и non-scope.
- [ ] Использовать канонические focused specs из `docs/methodology-layer/` как SoT baseline вместо legacy planning docs.
- [ ] Собрать и нормализовать requirements: `US-*`, `NFR-*`, `CONS-*`, `OQ-*`, при необходимости `R-*`.
- [ ] Подготовить единый spec document для `Project Methodology Runtime` с boundaries, architecture overview и implementation-ready sections.
- [ ] Выделить полный domain model: entities, value objects, relationships, invariants, lifecycle states.
- [ ] Забрать из legacy architecture draft remaining blocks, не вошедшие в focused specs: `drift detection`, `indexing`, `reconcile`, broader component framing, data flow and architect-stage follow-up topics.
- [ ] Спроектировать diagrams: component view, data flow, sync lifecycle, discovery flow, runtime materialization flow, graph relationship view.
- [ ] Зафиксировать contracts: MCP tools, Web UI actions, service-core API boundaries, config schemas, discovery schemas, graph query contracts.
- [ ] Спроектировать test design и coverage matrix для критичных flows, включая discovery, materialization, drift detection, traceability queries и cross-project navigation.
- [ ] Выявить архитектурные решения, требующие ADR, и оформить ADR pack.
- [ ] Пройти review gate и убедиться, что пакет Architect Stage не содержит скрытых предположений и готов к handoff в planning или implementation.

## Definition of Done
- [ ] Есть полный discovery output с `US-*`, `NFR-*`, `CONS-*`, `OQ-*`.
- [ ] Есть единый spec artifact, который можно использовать как основной архитектурный baseline для реализации.
- [ ] Есть завершенный domain model и согласованные diagrams.
- [ ] Есть contract-first артефакты для ключевых границ системы.
- [ ] Есть test design и coverage matrix для критичных требований.
- [ ] Есть ADR для ключевых архитектурных решений.
- [ ] Есть architect-stage review verdict и пакет готов к следующему этапу без больших пробелов.

## Execution Status
- Current State: Канонический SoT baseline для `Project Methodology Runtime` уже собран в `docs/methodology-layer/`; legacy planning package используется только как historical input для тех architect-stage blocks, которые еще не были подняты в implementation-ready artifacts.
- Next Step: Начать с Architect Discovery и нормализовать requirements в формальном виде `US-*`, `NFR-*`, `CONS-*`, `OQ-*` на основе уже принятых канонических документов слоя, а затем забрать remaining lifecycle and architect-stage framing из legacy architecture draft в новые stage artifacts.
- Blockers: none
- Contract Changes: none
- Verification: Проверить наличие итогового пакета артефактов по всем подэтапам из [`../../../../.kilocode/skills-architect/architect-stage/SKILL.md`](../../../../.kilocode/skills-architect/architect-stage/SKILL.md), включая spec, domain model, diagrams, contracts, test design, ADR и review-ready output.
