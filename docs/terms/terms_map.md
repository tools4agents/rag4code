# Карта терминов

> Status: Draft  
> Scope: каноническая карта терминов для документации HyperGraph  
> Role: краткий glossary для человека и агента с optional ссылками на детальные страницы

## 1. Назначение

Этот документ — каноническая карта терминов, используемых в документации проекта.

Он нужен для:
- lazy loading при чтении документации человеком и агентом;
- progressive disclosure от короткого определения к детальной странице термина;
- единообразной терминологии в архитектуре, методологии, контрактах и task-артефактах;
- уменьшения дублирования между документами.

## 2. Как пользоваться этим файлом

Используй эту страницу как первую точку входа, если в документе встречается важный термин.

Рекомендуемый маршрут чтения:
1. прочитать короткое определение здесь;
2. если у термина есть отдельная страница, открыть ее только при необходимости;
3. вернуться к исходному документу уже с общим пониманием смысла.

## 3. Правила для term pages

- `terms_map.md` хранит краткие канонические определения;
- большие, нагруженные или часто используемые термины могут получать отдельную страницу в `docs/terms/`;
- архитектурные и методологические документы должны ссылаться на эту карту, а не дублировать большие определения;
- контрактные документы используют ту же терминологию, но не пересказывают архитектурные объяснения.

## 4. Канонический реестр терминов

| Термин | Краткое определение | Детальная страница |
| --- | --- | --- |
| Project Methodology Runtime | Сервисный слой, который управляет methodology artifacts проекта, резолвит active methodology state, materialize environment-facing runtime files и поддерживает traceability через graph projection. | none |
| Source of Truth | Канонический источник состояния methodology. Для этого слоя это markdown и yaml files, а не database. | none |
| Central methodology catalog | Переиспользуемый catalog methodology artifacts, который хранится в service-local storage и связывается через stable identifiers, а не через project-local absolute paths. | none |
| Project Portable Intent | Переносимая project-owned configuration, которая задает methodology, versions, active artifacts, roles, profiles и discovery decisions без machine-specific absolute paths. | none |
| Service-local Runtime State | Внутреннее operational state сервиса: project runtime records, snapshots, jobs, caches и indices. | none |
| Runtime Materialization State | Environment-facing runtime projection, который потребляет agent system, например файлы в `.kilocode/` и другие generated runtime artifacts. | none |
| project-scoped runtime | Единый runtime view, materialized для конкретного проекта, чтобы агент видел один согласованный local layer, а не разрозненные global и project уровни. | none |
| portable references | Stable identifiers и relative references в project metadata вместо machine-specific physical paths. | none |
| MethodologyArtifact | Базовая generic artifact entity для слоя methodology runtime вместо hardcoded списка document kinds. | none |
| MethodologyArtifactType | Конфигурируемое описание artifact type, которое задает storage, graph semantics, rendering и validation expectations. | none |
| agent-system | ПО для работы с coding agents на базе LLM, у которого есть собственная модель `agent-role`, rules, tools и runtime artifacts, и под которое HyperGraph может готовить совместимые assets и выполнять materialization. | `docs/terms/project/terms/agent-system.md` |
| primary-agent-system | Выбранная разработчиком для работы с конкретным проектом основная `agent-system`, под которую HyperGraph materialize runtime и related environment-facing assets. В project configuration этот выбор фиксируется через поле `primary_agent_system`. | `docs/terms/project/terms/primary-agent-system.md` |
| role-pack | Reusable packaging unit для одной `agent-role`, которая объединяет abstract role artifact, `agent-system`-specific assets, docs и related metadata без смешения semantic boundaries. | `docs/terms/project/terms/role-pack.md` |
| knowledge-lifecycle asset | Asset type, который задает lifecycle знания в проекте: где оно рождается, где канонизируется и где публикуется для внешнего потребления. | `docs/terms/project/terms/knowledge-lifecycle-asset.md` |
| task-management-system asset | Asset type, который задает систему хранения, индексации и управления task artifacts. | `docs/terms/project/terms/task-management-system-asset.md` |
| terms-management-system asset | Asset type, который задает систему хранения, карты и progressive disclosure терминов. | `docs/terms/project/terms/terms-management-system-asset.md` |
| testing-system asset | Asset type, который задает систему хранения, индексации и traceability для testing documentation и links к test implementation. | `docs/terms/project/terms/testing-system-asset.md` |
| methodology asset | Asset type, который задает process model разработки: workflows, role usage, critique and review loops и другие methodology semantics. | `docs/terms/project/terms/methodology-asset.md` |
| composition pack | Совместимый publishable набор assets разных типов, который можно подключить как готовый методологический стек. | `docs/terms/project/terms/composition-pack.md` |
| agent-system-agnostic asset | Asset, который не зависит от конкретной `agent-system`, может использоваться как reusable source artifact до выбора runtime target и не содержит внутри себя `agent-system`-specific assets. | `docs/terms/project/terms/agent-system-agnostic-asset.md` |
| agent-system-specific asset | Asset, совместимый с конкретной `agent-system` на уровне представляемого артефакта и используемый как source layer для соответствующего runtime target. | `docs/terms/project/terms/agent-system-specific-asset.md` |
| agent-system materialization | Процесс, при котором HyperGraph раскладывает assets для выбранной `primary-agent-system` в конкретном проекте как runtime-facing artifacts. | `docs/terms/project/terms/agent-system-materialization.md` |
| agent-role | Общая role entity для agent environment. В Kilo Code `mode` — частный случай `agent-role`. | none |
| test-suite | Documentation unit, который объединяет связанный набор test cases, links на implementation roots и suite-level navigation metadata. | `docs/terms/project/terms/test-suite.md` |
| test-case | Минимальная documented verification unit внутри `test-suite`, которая имеет stable identifier и связывает requirement-level intent с конкретной test implementation. | `docs/terms/project/terms/test-case.md` |
| test-implementation | Code-level реализация test case в test module, test class или test function. | `docs/terms/project/terms/test-implementation.md` |
| repository-context-entry-model | Система входных точек и загрузки контекста проекта, которая задает `structure + navigation + ownership` для project-scoped agent work. | `docs/terms/project/terms/repository-context-entry-model.md` |
| nested-repo-context-switching | Правило переключения агента с parent project context на local context автономного nested project, когда task scope уходит внутрь этого repository. | `docs/terms/project/terms/nested-repo-context-switching.md` |
| manual-hybrid discovery | Discovery mode, в котором сервис heuristically находит candidates, а разработчик вручную подтверждает final classification. | none |
| project candidate | Директория, которую discovery heuristics определили как возможный project root, обычно по `.git` marker или другим project signals. | none |
| nested-project | Candidate внутри другого project root, который явно подтвержден как самостоятельный project в discovery configuration. | none |
| external-project-reference | Stable reference на другой project для navigation, integration или analysis, но не обязательно локально indexed как editable project. | none |
| service-managed-root | Директория, которой владеет сам сервис и которая исключается из обычной project discovery и indexing semantics. | none |
| graph projection | Derived graph representation в ArcadeDB для navigation, provenance и traceability, полностью rebuildable из source files. | none |
| drift detection | Сравнение desired runtime state и materialized runtime state для обнаружения mismatch, stale files или untracked manual edits. | none |
| reconcile | Процесс, который пересканирует source state, rebuild derived projections и при необходимости repair runtime materialization. | none |

## 5. Термины, которые должны быть строго синхронизированы между документами

Следующие термины должны использоваться во всех документах в одном и том же смысле:
- Project Methodology Runtime
- Source of Truth
- Central methodology catalog
- Project Portable Intent
- Service-local Runtime State
- Runtime Materialization State
- project-scoped runtime
- portable references
- MethodologyArtifact
- MethodologyArtifactType
- agent-system
- primary-agent-system
- role-pack
- knowledge-lifecycle asset
- task-management-system asset
- terms-management-system asset
- testing-system asset
- methodology asset
- composition pack
- agent-system-agnostic asset
- agent-system-specific asset
- agent-system materialization
- agent-role
- test-suite
- test-case
- test-implementation
- repository-context-entry-model
- nested-repo-context-switching
- manual-hybrid discovery
- external-project-reference
- graph projection
- drift detection
- reconcile

## 6. Политика обновления

Обновляй эту карту, если:
- новый повторяющийся термин появился в двух и более документах;
- термин изменил смысл или scope;
- появилась или была удалена отдельная term page;
- архитектурная миграция добавила новый canonical concept.

Этот файл — терминологическая точка входа для человека и агента.
