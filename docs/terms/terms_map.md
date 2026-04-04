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
| agent-role | Общая role entity для agent environment. В Kilo Code `mode` — частный случай `agent-role`. | none |
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
- agent-role
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