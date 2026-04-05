# Task: Консолидация и дедупликация planning-пакета для Project Methodology Runtime

## Контекст
- Источник: серия архитектурных обсуждений по `Project Methodology Runtime` в режиме Architect.
- Связанные артефакты:
  - [`docs/methodology-layer/artifact-model.md`](../../docs/methodology-layer/artifact-model.md)
  - [`docs/methodology-layer/workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md)
  - [`docs/methodology-layer/interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md)
  - [`docs/methodology-layer/project-discovery.md`](../../docs/methodology-layer/project-discovery.md)
  - [`operational_scope/ideas/project-first-model-and-storage.md`](../ideas/project-first-model-and-storage.md)
  - [`operational_scope/ideas/HyperGraph_vision.md`](../ideas/HyperGraph_vision.md)
  - [`operational_scope/ideas/integrated_knowledge_graph_schema.md`](../ideas/integrated_knowledge_graph_schema.md)

## Architecture Context References
- [ ] [`operational_scope/ideas/project-first-model-and-storage.md`](../ideas/project-first-model-and-storage.md)
- [ ] [`docs/adr/0001-arcadedb-as-unified-storage-for-mvp.md`](../../docs/adr/0001-arcadedb-as-unified-storage-for-mvp.md)

## Specification References
- [ ] [`docs/methodology-layer/overview.md`](../../docs/methodology-layer/overview.md)
- [ ] [`docs/methodology-layer/artifact-model.md`](../../docs/methodology-layer/artifact-model.md)
- [ ] [`docs/methodology-layer/workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md)
- [ ] [`docs/methodology-layer/interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md)
- [ ] [`docs/methodology-layer/project-discovery.md`](../../docs/methodology-layer/project-discovery.md)

## Test Design References
- [ ] `none` для этой задачи консолидации документации
- [ ] Зафиксировать gap, если в процессе понадобится отдельный Test Design artifact

## Workflow References
- [ ] `none`
- [ ] Подготовить ссылку на workflow позже, если в ходе консолидации будет создан отдельный planning workflow

## Цель
- Привести planning-пакет по `Project Methodology Runtime` к единому, непротиворечивому и недублирующему baseline.
- Устранить рассинхроны между документами и зафиксировать единую терминологию, единые Source of Truth boundaries и единые правила ссылок между документами.
- Подготовить пакет документов так, чтобы его можно было безопасно продолжать в новом чате или передать другому Architect agent без потери контекста.

## Ключевой контекст для продолжения
- Legacy planning-пакет в `operational_scope/plans/` уже использован как buffer-источник для миграции в канонические focused specs слоя.
- Уже созданы канонические документы [`docs/methodology-layer/artifact-model.md`](../../docs/methodology-layer/artifact-model.md), [`docs/methodology-layer/workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md), [`docs/methodology-layer/interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md) и [`docs/methodology-layer/project-discovery.md`](../../docs/methodology-layer/project-discovery.md).
- Пользователь отдельно подтвердил, что `docs/` является SoT, а planning и discussion artifacts являются buffer-слоем и после миграции должны очищаться.
- Принятые решения, которые должны быть единообразно отражены во всех документах:
  - Source of Truth для methodology artifacts — markdown и yaml files.
  - `Central methodology catalog` живет во внутреннем storage сервиса, путь задается service settings, но не хранится в project metadata.
  - Project хранит только portable references без machine-specific absolute paths.
  - Runtime для agent system materialize как единый project-scoped local layer.
  - Базовая meta-model строится через `MethodologyArtifact` и `MethodologyArtifactType`, а не через жесткий список kinds.
  - Базовые baseline types: `methodology-doc`, `rule-doc`, `skill-doc`, `agent-role`.
  - `agent-role` — общая сущность; в Kilo Code частный случай — `mode`.
  - Web UI в первой итерации нужен для graph navigation, project configuration и получения path к artifact file, но не как markdown viewer/editor.
  - MCP нужен для traceability, navigation, role awareness, artifact resolution, project term lookup, links между ADR, user story, contract, tests и components.
  - `Project Discovery` первой итерации — manual-hybrid: сервис ищет candidates, разработчик вручную классифицирует, результат сохраняется в project config, автоматического rediscovery нет.
  - Вложенный `.git` по умолчанию считается `project candidate`, но финальную классификацию определяет разработчик.
  - `external-project-reference` — это внешний проект, важный для интеграции и анализа, но не обязательно локально индексируемый как редактируемый проект.
  - Минимальный graph contract первого MVP для проектов должен оставаться простым: `Project` nodes, признак `has_local_db`, edges `USES_PROJECT` и `PARENT_OF`.

## Шаги реализации
- [ ] Прочитать и сопоставить четыре planning-документа как единый пакет.
- [ ] Составить список противоречий, дублей и терминологических расхождений.
- [ ] Для каждого спорного вопроса выбрать один canonical baseline и зафиксировать его во всех затронутых документах.
- [ ] Привести к единой терминологии как минимум следующие понятия: `Source of Truth`, `Project Portable Intent`, `Service-local Runtime State`, `Runtime Materialization State`, `MethodologyArtifactType`, `agent-role`, `manual-hybrid discovery`, `external-project-reference`, `project-scoped runtime`, `portable references`.
- [ ] Убрать дублирование больших блоков, оставив в каждом документе только его непосредственную ответственность и ссылки на соседние документы.
- [ ] Проверить, что нигде не осталось противоречий по storage boundary, discovery policy, graph contract, central catalog location, nested `.git` policy и adapter semantics.
- [ ] При необходимости создать один короткий consolidation summary document с навигацией по итоговому planning-пакету.

## Definition of Done
- [ ] Четыре planning-документа согласованы между собой и не содержат явных противоречий.
- [ ] Ключевые термины используются единообразно.
- [ ] Дублирование между документами уменьшено, а границы ответственности файлов стали яснее.
- [ ] Зафиксирован единый baseline для дальнейшего Architect stage.
- [ ] Пакет документов пригоден для продолжения работы в новом чате без дополнительных устных пояснений.

## Execution Status
- Current State: Канонические focused specs для `Project Methodology Runtime` уже созданы в `docs/methodology-layer/`; идет cleanup legacy planning и discussion artifacts, а также синхронизация task-buffer с новым SoT.
- Next Step: Обновить оставшиеся task and ADR references, затем очистить временные artifacts из `operational_scope/plans/` и `operational_scope/discussion/` после финальной проверки ссылок.
- Blockers: none
- Contract Changes: none
- Verification: Сверить [`docs/methodology-layer/overview.md`](../../docs/methodology-layer/overview.md), [`docs/methodology-layer/artifact-model.md`](../../docs/methodology-layer/artifact-model.md), [`docs/methodology-layer/workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md), [`docs/methodology-layer/interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md) и [`docs/methodology-layer/project-discovery.md`](../../docs/methodology-layer/project-discovery.md) и убедиться, что решения по SoT, discovery, graph contract, role separation и terminology совпадают.
