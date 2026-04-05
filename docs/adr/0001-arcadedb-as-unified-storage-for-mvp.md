# ADR-0001: ArcadeDB as unified storage engine for HyperGraph MVP

## Status
- **Accepted** (for MVP)
- **Date**: 2026-03-08

## Context

HyperGraph развивает модель **Project-first**: проект — это `project_root` с ровно одним Git-репозиторием, без nested repos, с хранением путей артефактов как relative paths от `project_root`.

Для MVP нам важно быстро показать возможности HyperGraph:
- работать с данными **как с графом** (traversal: backlinks, dependency graph, bridges)
- иметь **SQL** для operational state (индекс файлов/чекпоинты/диагностика)
- иметь **Vector** слой (embeddings + similarity search)
- иметь **KV** слой (например, термины проекта / словарь / настройки)

При этом требования:
- open source
- Docker + volumes (персистентность)
- per-project изоляция
- минимальная Ops-сложность для разработки и демонстрации

См. сравнительные заметки:
- [`operational_scope/research/db-overview/arcade_db.md`](../../operational_scope/research/db-overview/arcade_db.md)
- [`operational_scope/research/db-overview/multi_db.md`](../../operational_scope/research/db-overview/multi_db.md)

## Decision

Для MVP выбираем **ArcadeDB** как единый multi-model storage engine.

### Deployment / isolation
- **Один ArcadeDB container** на HyperGraph runtime.
- Внутри инстанса: **`1 project -> 1 ArcadeDB database`**.
- Backup/restore: на уровне **database folder** (каталог БД на примонтированном volume).

### Logical model (portable)
При этом в документации и архитектуре мы сохраняем **логическую модель** независимых слоёв:
- **SQL Store**: operational state (file-change index, checkpoints, diagnostics)
- **Graph Store**: nodes/edges, traversal, bridges
- **Vector Store**: embeddings + similarity search
- **KV Store**: небольшой key/value слой (термины проекта, словари, настройки)

В MVP **все эти логические хранилища реализуются внутри одной ArcadeDB database**.

### Why
- Максимальная скорость итераций MVP: один движок закрывает несколько моделей данных.
- Упрощение эксплуатации dev/demo: один контейнер, единый volume, единые процедуры старта.

### Additional MVP advantage: reuse of existing tooling and drivers

ArcadeDB поддерживает несколько протоколов/языков, что позволяет на этапе MVP:
- подключать привычные инструменты и драйверы (например, через Postgres/Redis/MongoDB совместимые клиенты)
- ускорять эксперименты и миграции запросов между парадигмами (SQL/Cypher/Gremlin)

Оговорка:
- это следует рассматривать как **integration leverage**, а не как гарантированную полную эмуляцию всех особенностей соответствующих СУБД.

## Alternatives considered

### A) FalkorDB (graph) + PostgreSQL (SQL) + отдельный vector store
Плюсы:
- сильный graph слой и multi-graph изоляция

Минусы:
- polyglot persistence (несколько движков) усложняет консистентность, бэкапы и диагностику

См. сравнение: [`operational_scope/research/db-overview/glm_research.md`](../../operational_scope/research/db-overview/glm_research.md)

### B) PostgreSQL + Apache AGE + pgvector
Плюсы:
- единая зрелая платформа PostgreSQL, сильный Python-стек
- изоляция per-project через отдельные PostgreSQL DB

Минусы:
- AGE как extension требует аккуратной матрицы версий и может быть менее удобен как “native graph”

См. сравнение: [`operational_scope/research/db-overview/qwen_research.md`](../../operational_scope/research/db-overview/qwen_research.md)

### C) No-op / best-of-breed
Например: PostgreSQL (SQL) + Neo4j CE (graph) + Qdrant (vector).

Минусы:
- максимальная Ops-сложность для MVP
- сложнее обеспечить “быстро показать возможности”

## Consequences

### Positive
- MVP быстрее по time-to-demo.
- Единая точка хранения на проект (в пределах одной ArcadeDB database).

### Negative / risks
- JVM-centric стек.
- Python интеграция может требовать дополнительных обвязок (HTTP API / community drivers).
- Риск lock-in в multi-model API (если начнём активно использовать уникальные фичи без abstraction слоя).
- Риск “ложной совместимости”: wire-protocol совместимость может не покрывать 100% семантики конкретных СУБД.

## Review conditions (when to revisit)

Пересматриваем решение и мигрируем на PostgreSQL + плагины (AGE + pgvector), если выполняется хотя бы одно:
- проблемы стабильности/персистентности/backup-restore
- недостаточная эргономика Python SDK
- проблемы производительности на наших типовых запросах (bulk upsert, traversal, vector search)
- сложность поддержки/обновления ArcadeDB выше ожидаемой

## Migration plan (fallback)

Чтобы migration был реалистичным, в реализации придерживаемся принципов:
1. Вводим storage-абстракции на уровне HyperGraph (SQL/Graph/Vector/KV interfaces).
2. Держим схемы и данные максимально переносимыми (не завязываемся на vendor-only конструкции без необходимости).
3. Обеспечиваем export/import для сущностей MVP (Artifacts, Links, Terms, Embeddings).

## Related documents
- Platform invariants: [`operational_scope/ideas/project-first-model-and-storage.md`](../../operational_scope/ideas/project-first-model-and-storage.md)
- Obsidian Assistant architecture: [`services/obsidian-assistant/docs/spec/architecture.md`](../../services/obsidian-assistant/docs/spec/architecture.md)
- Hyper Project Memory strategy: [`services/hyper-project-memory/docs/execution/plans/architecture-graph-git-versioning-strategy.md`](../../services/hyper-project-memory/docs/execution/plans/architecture-graph-git-versioning-strategy.md)
