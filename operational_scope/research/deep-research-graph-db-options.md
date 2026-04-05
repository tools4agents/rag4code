# Deep Research Task: Open-source Graph DB for HyperGraph (Project-first, per-project isolation)

## 1) Goal
Выбрать графовую БД (или связку решений) для HyperGraph, которая:

- **Open Source** и доступна всем участникам (без платных/enterprise-only фич как критической зависимости).
- Поддерживает **изоляцию на уровне проекта**: *1 проект → отдельная графовая БД* (логически и желательно физически).
- Умеет жить в **Docker** и восстанавливаться после выключения ПК за счет **persisted volumes**.
- Позволяет построить **web-визуализацию графа** (минимум: nodes/edges, фильтры, traversal) для фронтенда наших инструментов.

Результат исследования должен дать рекомендацию для MVP и roadmap на расширение.

## 2) Background / Context (почему это важно)

### 2.1 HyperGraph vision
HyperGraph строится как граф знаний, объединяющий:
- docs graph (markdown)
- code graph (static analysis + LSP)
- tasks/workflow/memory layer

Источник истины: файлы (Git). Проекции: SQL operational state и graph query store.

См.:
- `operational_scope/ideas/HyperGraph_vision.md`
- `services/hyper-project-memory/docs/execution/plans/architecture-graph-git-versioning-strategy.md`

### 2.2 Project-first модель (уточнено в обсуждении)
Проект:
- это путь к директории
- внутри ровно один `.git` (без nested repos)

Вложенный проект:
- задается как **ссылка на внешний путь**
- в потребляющем проекте выглядит как **абстрактный компонент** с интерфейсами/API
- но у него есть `project_id`, и мы можем *switch(project_id)* чтобы открыть внутренности

### 2.3 Storage boundary
Изоляция на проект:
- 1 project → отдельная PostgreSQL DB
- 1 project → отдельная Graph DB

При этом допускается, что runtime сервис один (например, один docker контейнер/DBMS), но внутри создаются отдельные базы на проекты.

## 3) MVP scope

### 3.1 Obsidian links MVP
Важно только:
- **ссылки между заметками**
- **только markdown ссылки** (`[]()`)
- хранить пути относительно корня проекта

### 3.2 Core graph queries
Нужны базовые операции:
- outgoing/incoming links
- broken/unresolved links
- traversal (neighbors, paths up to depth)

## 4) Constraints / Non-goals

### 4.1 Constraints
- Только Open Source / доступные всем возможности.
- Деплой в Docker с volume persistence.
- Python-friendly (драйвер/SDK), чтобы Core сервисы могли писать/читать graph.
- Возможность организовать *per-project isolation* без Enterprise лицензий.

### 4.2 Non-goals (на первом шаге)
- Кластера/HA/enterprise security.
- Сложные граф-алгоритмы (GDS) как обязательное требование.

## 5) Research Questions (ответы с источниками)

### 5.1 Кандидаты на роль Graph DB
Найти и сравнить кандидатов (не ограничиваться списком):

1) **Neo4j Community**
   - поддерживает ли multi-database per DBMS в community?
   - если нет: можно ли делать per-project isolation через отдельные контейнеры/инстансы?
   - что есть для open-source визуализации (не Bloom)?

2) **Memgraph**
   - лицензия и ограничения
   - есть ли multi-database / multi-tenancy в OSS редакции
   - Memgraph Lab: open-source ли, можно ли встраивать/переиспользовать

3) **Apache AGE (PostgreSQL extension)**
   - зрелость и ограничения
   - подходит ли как замена отдельной Graph DB (graph внутри Postgres DB)
   - насколько удобен Cypher/операции traversal
   - как будет выглядеть web-визуализация в этом варианте

4) **NebulaGraph / Dgraph / JanusGraph / Kuzu / FalkorDB / OrientDB**
   - лицензия
   - режим хранения (persistent / in-memory + WAL)
   - docker images и поддержка volumes
   - query language (cypher/gremlin/graphql/свой)
   - есть ли web UI или удобные интеграции

### 5.2 Изоляция per-project без enterprise
Проверить для каждого кандидата:
- Возможность создать **отдельную базу/граф** для проекта внутри одного DBMS.
- Если недоступно: какой лучший open-source способ обеспечить изоляцию?
  - отдельные инстансы/контейнеры
  - отдельные volumes
  - namespace/labels (как fallback)

### 5.3 Визуализация графа в web frontend
Нам важна не столько встроенная UI БД, сколько возможность:
- строить web UI внутри наших инструментов
- делать интерактивные выборки и traversal

Нужно исследовать варианты:
- Open-source JS libs (Cytoscape.js, Sigma.js, vis-network и т.п.)
- есть ли готовые open-source UI для выбранных графовых БД
- best practice: хранение vs визуализация (не связывать выбор БД с наличием “вендор UI”)

### 5.4 Persistence / backup / restore
Для каждого кандидата:
- как обеспечивается сохранение данных на volumes
- как делаются backup/restore (минимальный сценарий)
- совместимость с “выключили ПК → включили → подняли контейнеры”

### 5.5 API / SDK
Для каждого кандидата:
- Python driver наличие и качество
- транзакции
- bulk upsert/merge patterns
- delete+insert outgoing edges per source (важно для инкрементального sync)

## 6) Deliverables

1) Таблица сравнения (минимум столбцы):
- Candidate
- License
- Multi-DB per server (OSS)
- Docker + volumes
- Python driver
- Query language
- Backup/restore
- Visualization options
- Риски/ограничения

2) Рекомендация:
- 1 выбор для MVP
- 1-2 альтернативы (если MVP упирается в ограничения)

3) Предложение по интеграции в наш паттерн:
- 1 project → 1 SQL DB + 1 Graph DB
- как будет работать `switch(project_id)`
- как хранить относительные пути

4) Список ссылок-источников (официальные docs/репозитории/issue threads).

## 7) Output Format
Ответ оформить как markdown-отчет, чтобы его можно было положить в `docs/` или `plans/`.

## 8) Context Files (read-first)
Минимальный набор артефактов, которые нужно прочитать перед выводами:

- HyperGraph vision: `../ideas/HyperGraph_vision.md`
- Integrated schema: `../ideas/integrated_knowledge_graph_schema.md`
- Obsidian Assistant architecture: `../../services/obsidian-assistant/docs/spec/architecture.md`
- Obsidian Assistant indexing strategy: `../../services/obsidian-assistant/docs/spec/indexing.md`
- Hyper Project Memory: `../../services/hyper-project-memory/README.md`
- Git-authoritative + projections: `../../services/hyper-project-memory/docs/execution/plans/architecture-graph-git-versioning-strategy.md`
- Pain points: graph index for markdown links: `/home/anton-admin/.kilocode/plans/ai-self-reflection-report-graph-links.md`
