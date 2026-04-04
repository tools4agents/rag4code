# Open-source Graph DB for HyperGraph (Project-first, per-project isolation)

## 0. Краткий вывод

**Рекомендация для MVP:**

1. **FalkorDB** (основной выбор)  
   - Open-source, permissive-лицензия, **полная multi-tenancy в OSS** (много графов в одном инстансе)【turn58fetch0】.  
   - OpenCypher, хорошая Python-поддержка (`falkordb-py` + OGM)【turn51fetch0】【turn49fetch0】.  
   - Легко живёт в Docker с персистентностью через Redis/RDB/append-only files【turn64fetch0】.  
   - Есть готовый web UI (FalkorDB Browser) и MCP-сервер для интеграции с AI-инструментами【turn49fetch0】【turn55search3】.

2. **Apache AGE** (альтернатива, если хотите единую PostgreSQL-платформу)  
   - PostgreSQL-расширение, граф внутри уже привычной SQL-БД【turn21fetch0】.  
   - OpenCypher поверх SQL, работает с `psycopg2`/`apache-age-python`【turn44fetch0】.  
   - Идеально, если хотите **1 project → 1 PostgreSQL DB + 1 graph-схема внутри**.

3. **Neo4j Community** (третий вариант, если принципиально отдельный сервер Neo4j)  
   - Отличный Python-драйвер, зрелый Cypher, встроенный Neo4j Browser【turn43fetch0】【turn56search3】.  
   - Но **нет multi-DB в Community** — изоляция только через отдельные контейнеры/инстансы【turn8fetch0】.  
   - Для MVP это можно пережить, но масштабировать до десятков проектов будет неудобно.

---

## 1. Сравнительная таблица кандидатов

### 1.1 Основные кандидаты

| Candidate | License | Multi-DB per server (OSS) | Docker + volumes | Python driver | Query language | Backup/restore (OSS) | Visualization options | Риски/ограничения |
|----------|---------|---------------------------|------------------|---------------|----------------|----------------------|-----------------------|-------------------|
| **FalkorDB** | Apache-2.0 / BSD (клиенты)【turn25search3】【turn25search4】【turn51fetch0】 | **Да** – несколько графов (graph keys) в одном инстансе; multi-tenancy полностью в OSS【turn58fetch0】 | Официальный Docker-образ `falkordb/falkordb`【turn64fetch0】; персистентность через Redis persistence (RDB/AOF) | Официальный Python-клиент `falkordb-py` + OGM `falkordb-py-orm`【turn51fetch0】 | OpenCypher с расширениями【turn55search1】【turn55search2】 | Стандартные Redis-механизмы: RDB snapshots, AOF; возможен `GRAPH.DELETE` + повторная загрузка из CSV/JSON | Есть web UI (FalkorDB Browser)【turn49fetch0】, MCP-сервер【turn55search3】; в своём UI можно использовать любые JS-libs (Cytoscape.js, Sigma.js и т.п.) | Относительно молодой проект; меньше “боевого” опыта, чем у Neo4j, но активное развитие. |
| **Apache AGE** | Apache-2.0【turn0search12】 | **Да** – несколько графов в одной PostgreSQL БД (`create_graph('graph_name')`)【turn21fetch0】 | Официальный Docker-образ `apache/age`【turn21fetch0】; внутри обычный Postgres, volumes стандартно | Python-драйвер `apache-age-python`, работает через `psycopg2`【turn44fetch0】 | OpenCypher внутри SQL (`SELECT * FROM cypher('graph_name', $$ ... $$)`)【turn21fetch0】 | Стандартные `pg_dump`/`pg_restore` для БД с AGE-схемами【turn22search10】 | Встроенного web UI нет; визуализацию строить на своём фронтенде (JS libs) + SQL/AGE endpoint | Меньше “графовых” фич (нет готовых GDS, ограниченный инструментарий); сложнее отладка Cypher+SQL. |
| **Neo4j Community** | GPL (CE)【turn0search3】 | **Нет** – один DB на инстанс; multi-DB только в Enterprise【turn8fetch0】 | Официальный Docker-образ, персистентность через volume `/data`【turn37fetch0】 | Официальный Python-драйвер `neo4j-driver` ( Bolt )【turn43fetch0】 | Cypher | Оффлайн backup: `neo4j-admin database dump/load` или просто копия `/data`【turn22search0】【turn22search3】 | Встроенный Neo4j Browser (в т.ч. в CE)【turn56search3】; есть open-source NeoDash (dashboards)【turn56search0】 | Multi-DB только через отдельные инстансы/контейнеры; GPL-лицензия может быть ограничением для коммерческого использования. |
| **Memgraph** | Open-source (GPL/коммерческая)【turn0search9】 | **Multi-tenancy только в Enterprise**【turn0search5】【turn0search6】 | Docker-образ, персистентность через WAL + snapshots【turn42fetch0】 | GQLAlchemy (OGM для Memgraph/Neo4j)【turn15search1】【turn15search3】 | Cypher | Snapshots + WAL в data-директории【turn42fetch0】 | Memgraph Lab (web UI)【turn23search0】 | Multi-DB в OSS недоступна; для изоляции нужно несколько инстансов или контейнеров. |
| **NebulaGraph** | Apache-2.0【turn3search7】【turn3search8】 | **Да** – graph spaces физически изолированы, аналог “баз данных”【turn54find0】 | Есть Docker-образ; backup/restore через BR tool (OSS)【turn22search16】 | Python-клиент `nebula3-python`【turn2search3】 | nGQL (OpenCypher-подобный) | BR tool для backup/restore graph spaces【turn22search16】 | Nebula Studio (web GUI)【turn17fetch0】 | Распределённая архитектура, сложнее в настройке для локального/dev-режима; более “ops-heavy”. |
| **Kuzu** | MIT (permissive)【turn25search0】 | **Нет** – embedded DB, 1 файл = 1 граф; multi-DB через несколько файлов/процессов | Docker-образы `kuzudb/api-server`, `kuzudb/explorer`【turn26fetch0】; можно просто файл на volume | Python-пакет `kuzu` (embedded, in-process)【turn61fetch0】【turn63search0】 | Cypher | Бэкап = копия файла БД; есть экспорт в CSV/Parquet【turn61fetch0】 | Kuzu Explorer (web UI)【turn26fetch0】【turn59search1】 | Embedded-подход: нужно продумать lifecycle процессов/файлов; меньше подходит, если нужен отдельный серверный процесс. |
| **Dgraph** | AGPL + Commons Clause (не OSI-approved open source)【turn9search0】 | Несколько пространств имён (namespaces), но есть нюансы по лицензии | Docker-образ `dgraph/dgraph`【turn2search6】 | Python-клиент `pydgraph`【turn2search5】 | GraphQL | Backup через экспорт/импорт, есть механизмы snapshots | Встроенного UI нет; сторонние решения | Лицензия AGPL + Commons Clause — это **не классический open source**; могут быть ограничения для коммерческого использования. |
| **OrientDB** | Apache-2.0 (Community)【turn3search10】【turn3search13】 | Поддержка нескольких баз (документно-графовых) | Docker-образ; персистентность через файлы БД | Java/Python-драйверы (TinkerPop/Gremlin) | SQL + Gremlin | Backup через экспорт/импорт или копию файлов | OrientDB Studio (web UI)【turn3search11】 | Менее активное развитие по сравнению с Neo4j/FalkorDB; более сложная экосистема. |

---

## 2. Детали по ключевым кандидатам

### 2.1 FalkorDB

**Лицензия и open-source**

- FalkorDB – open-source property graph DB, лицензии Apache-2.0 / BSD для клиентов【turn25search3】【turn25search4】【turn51fetch0】.  
- Multi-tenancy (много графов в одном инстансе) **полностью доступна в OSS**【turn58fetch0】.

**Multi-DB / изоляция проектов**

- Каждый граф идентифицируется своим **graph key** (имя графа).  
- Запрос всегда выполняется в контексте одного графа; cross-graph запросы не поддерживаются【turn58fetch0】.  
- Это идеально ложится на модель **1 project → 1 graph key** внутри одного FalkorDB-инстанса.

**Docker + persistence**

- Официальный Docker-образ `falkordb/falkordb`【turn64fetch0】.  
- FalkorDB работает поверх Redis; персистентность обеспечивается стандартными механизмами Redis:
  - RDB snapshots;
  - AOF (append-only file);
  - можно делать бэкапы через Redis RDB + `GRAPH.DELETE` + повторную загрузку.

**Python-драйвер**

- Официальный Python-клиент `falkordb-py` (MIT)【turn51fetch0】.  
- Есть ORM `falkordb-py-orm`【turn51fetch0】.  
- Для локальной разработки/CI есть **FalkorDBLite** – embedded вариант, запускается как subprocess, без Docker и конфигурации【turn27fetch0】【turn30search0】.

**Query language**

- OpenCypher с расширениями【turn55search1】【turn55search2】.  
- Для ваших сценариев (Obsidian links, traversal) этого достаточно.

**Backup/restore**

- В OSS – стандартные Redis-механизмы (RDB/AOF).  
- Можно делать логические бэкапы:
  - выгрузка в CSV/JSON через собственные скрипты;
  - загрузка обратно через `GRAPH.QUERY` или bulk-загрузку.

**Visualization**

- Есть **FalkorDB Browser** – web UI для работы с графами【turn49fetch0】.  
- Есть MCP-сервер для интеграции с LLM-агентами【turn55search3】.  
- Для собственного UI можно использовать:
  - **Cytoscape.js** – JS-библиотека для визуализации графов【turn45search0】【turn45search2】;
  - **Sigma.js** + Graphology – WebGL-рендеринг для больших графов【turn45search5】【turn45search6】;
  - **vis-network** – простая сеть “из коробки”【turn45search10】【turn45search12】.

---

### 2.2 Apache AGE

**Лицензия и зрелость**

- Apache AGE – PostgreSQL-расширение, Apache-2.0【turn0search12】.  
- Входит в Apache Incubator и позднее стал Top-Level Project (2022)【turn0search12】.

**Multi-DB / изоляция**

- В одной PostgreSQL-БД можно создавать несколько графов:
  ```sql
  SELECT create_graph('graph_name');
  SELECT * FROM cypher('graph_name', $$ ... $$) AS (v agtype);
  ```
- Это даёт **1 project → 1 graph** в рамках одной PostgreSQL-БД.

**Docker + persistence**

- Официальный Docker-образ `apache/age`【turn21fetch0】.  
- Внутри – обычный PostgreSQL; persistence через стандартные volume для PGDATA.

**Python-драйвер**

- Python-драйвер `apache-age-python`, работает поверх `psycopg2`【turn44fetch0】.  
- Примеры подключения есть в блоге Apache AGE【turn44fetch0】.

**Query language**

- OpenCypher внутри SQL (`cypher()` function)【turn21fetch0】.  
- Для traversal это удобно, но отладка сложнее, чем в “чистых” графовых БД.

**Backup/restore**

- Стандартные `pg_dump`/`pg_restore` для БД с AGE-схемами【turn22search10】.  
- Миграция между версиями PostgreSQL также поддерживается【turn22search10】.

**Visualization**

- Встроенного web UI нет.  
- Для визуализации нужно:
  - писать SQL/AGE-запросы;
  - отдавать результаты через API;
  - рисовать граф на фронтенде (Cytoscape.js, Sigma.js, vis-network).

---

### 2.3 Neo4j Community

**Лицензия и ограничения**

- Neo4j Community Edition – GPL.  
- Multi-DB **только в Enterprise**; в CE поддерживается только одна БД на инстанс【turn8fetch0】.

**Multi-DB / изоляция проектов**

- Официальная рекомендация для multi-tenancy в CE:
  - **контейнер/инстанс на проект**【turn8fetch0】;
  - или использование labels/namespace для логической изоляции.

**Docker + persistence**

- Официальный Docker-образ Neo4j.  
- Персистентность: volume `/data` хранит все файлы БД【turn37fetch0】.

**Python-драйвер**

- Официальный Python-драйвер `neo4j-driver` (Bolt)【turn43fetch0】.  
- Отличная документация и примеры.

**Query language**

- Cypher – де-факто стандарт.

**Backup/restore**

- В CE – оффлайн backup:
  - `neo4j-admin database dump/load`【turn22search0】【turn22search1】;
  - или просто копия `/data` при остановленном контейнере【turn22search3】.

**Visualization**

- Neo4j Browser – встроенный UI для Cypher и визуализации【turn56search3】.  
- NeoDash – open-source dashboard builder для Neo4j【turn56search0】.  
- Для собственного UI можно использовать те же JS-библиотеки (Cytoscape.js, Sigma.js).

---

### 2.4 Memgraph

**Лицензия**

- Open-source (GPL) + коммерческая Enterprise-версия.  
- Multi-tenancy – **только в Enterprise**【turn0search5】【turn0search6】.

**Multi-DB / изоляция**

- В OSS – только одна БД на инстанс.  
- Для изоляции проектов нужно:
  - несколько контейнеров/инстансов Memgraph.

**Docker + persistence**

- Memgraph Docker-образ, персистентность через:
  - WAL + периодические snapshots【turn42fetch0】.

**Python-драйвер**

- GQLAlchemy – OGM для Memgraph и Neo4j【turn15search1】【turn15search3】.  
- Поддержка Python есть.

**Query language**

- Cypher (совместимость с Neo4j).

**Backup/restore**

- Snapshots + WAL; можно копировать data-директорию.

**Visualization**

- Memgraph Lab – web UI для визуализации и администрирования【turn23search0】.

**Почему не основной выбор**

- Multi-tenancy недоступна в OSS → не соответствует требованию “изоляция на уровне проекта без Enterprise-зависимости”.

---

### 2.5 NebulaGraph

**Лицензия**

- Apache-2.0【turn3search7】【turn3search8】.

**Multi-DB / изоляция**

- Graph spaces – физически изолированные графы, аналог “баз данных”【turn54find0】.  
- Это хорошо ложится на модель **1 project → 1 graph space**.

**Docker + persistence**

- Есть Docker-образ; backup/restore через BR tool (OSS)【turn22search16】.

**Python-драйвер**

- Python-клиент `nebula3-python`【turn2search3】.

**Query language**

- nGQL (OpenCypher-подобный)【turn3search7】.

**Visualization**

- Nebula Studio – web GUI【turn17fetch0】.

**Риски**

- Распределённая архитектура, сложнее в локальном/dev-режиме.  
- Для MVP с одним инстансом это избыточно.

---

### 2.6 Kuzu

**Лицензия**

- MIT (permissive)【turn25search0】.

**Архитектура**

- Embedded graph DB, in-process, файл на диске【turn61fetch0】.  
- Columnar disk-based storage, CSR-индексы.

**Multi-DB / изоляция**

- 1 файл БД = 1 граф; multi-DB через:
  - несколько файлов;
  - несколько процессов Kuzu.

**Docker + persistence**

- Docker-образы `kuzudb/api-server`, `kuzudb/explorer`【turn26fetch0】.  
- Можно использовать Kuzu как embedded-библиотеку без Docker.

**Python-драйвер**

- Python-пакет `kuzu` (embedded)【turn61fetch0】【turn63search0】.

**Query language**

- Cypher.

**Visualization**

- Kuzu Explorer – web UI【turn26fetch0】【turn59search1】.

**Риски**

- Embedded-подход требует careful lifecycle management процессов/файлов.  
- Для серверного режима нужна собственная обвязка (API-server уже есть【turn26fetch0】).

---

## 3. Изоляция per-project без Enterprise

### 3.1 FalkorDB

- **Нативная multi-tenancy в OSS**:
  - каждый проект – отдельный graph key (`project_id` как имя графа);
  - запросы всегда идут к конкретному графу;
  - физическая изоляция данных на уровне key-space【turn58fetch0】.
- Это **идеальное соответствие** требованию “1 project → 1 graph DB”.

### 3.2 Apache AGE

- **Граф внутри PostgreSQL-БД**:
  - 1 project → 1 PostgreSQL-БД;
  - внутри БД – 1 граф (или несколько графов, если нужно).
- Для изоляции можно:
  - использовать разные PostgreSQL-БД (как у вас уже планируется);
  - либо разные графы внутри одной БД (если проекты небольшие).

### 3.3 Neo4j Community

- **Нет multi-DB в CE**:
  - 1 project → 1 Neo4j-контейнер/инстанс【turn8fetch0】.
- Для dev-режима:
  - docker-compose с сервисами вида `neo4j_project_1`, `neo4j_project_2`;
  - volumes `neo4j_project_1_data`, `neo4j_project_2_data`.
- Это увеличивает оперативные накладные расходы, но для MVP допустимо.

---

## 4. Визуализация графа в web frontend

### 4.1 Open-source JS-библиотеки

- **Cytoscape.js** – JS-библиотека для визуализации графов, активно используется в Knowledge Graph-проектах【turn45search0】【turn45search2】.  
- **Sigma.js** + Graphology – WebGL-рендеринг, хорош для больших графов【turn45search5】【turn45search6】.  
- **vis-network** – простая сеть, удобна для начала【turn45search10】【turn45search12】.

### 4.2 Готовые UI

- **FalkorDB Browser** – web UI для работы с несколькими графами【turn49fetch0】.  
- **Neo4j Browser** – встроенный UI для Neo4j【turn56search3】.  
- **Nebula Studio**, **Memgraph Lab**, **Kuzu Explorer** – аналогичные UI для своих БД.

### 4.3 Best practice

- **Не привязывать выбор БД к наличию “вендорского UI”**:
  - БД выбираем по данным, изоляции и транзакциям;
  - UI – отдельно: либо свой на Cytoscape/Sigma/vis, либо готовый (Browser/Lab/Studio).

---

## 5. Persistence / backup / restore

### 5.1 FalkorDB

- Персистентность через Redis (RDB/AOF).  
- Backup:
  - периодические RDB-снапшоты Redis;
  - логический бэкап через экспорт в CSV/JSON и последующую загрузку.

### 5.2 Apache AGE

- Standard PostgreSQL backup:
  - `pg_dump` / `pg_restore` для БД с AGE-схемами【turn22search10】.

### 5.3 Neo4j Community

- Оффлайн backup:
  - `neo4j-admin database dump/load`【turn22search0】【turn22search1】;
  - или копия `/data` при остановленном контейнере【turn22search3】.

---

## 6. API / SDK и паттерны работы

### 6.1 FalkorDB

- Python-клиент `falkordb-py` + ORM【turn51fetch0】.  
- Транзакции – на уровне Redis (multi-exec).  
- Bulk upsert/merge:
  - загрузка из CSV/JSON через `GRAPH.QUERY` или собственные скрипты;
  - для инкрементального sync – delete/insert по условиям.

### 6.2 Apache AGE

- Python-драйвер `apache-age-python`【turn44fetch0】.  
- Транзакции – PostgreSQL-транзакции.  
- Bulk load:
  - `load_labels_from_file`, `load_edges_from_file`【turn31search0】.

### 6.3 Neo4j Community

- Официальный Python-драйвер `neo4j-driver`【turn43fetch0】.  
- Транзакции, batch-операции, merge/upsert через Cypher.

---

## 7. Рекомендация и архитектура интеграции

### 7.1 Выбор для MVP

**FalkorDB** как основной выбор:

1. **Open-source multi-tenancy** – изоляция проектов через graph keys без Enterprise-зависимости【turn58fetch0】.  
2. OpenCypher, что упрощает миграцию знаний/кода из Neo4j.  
3. Хороший Python-стек: `falkordb-py`, ORM, FalkorDBLite для локальной разработки【turn51fetch0】【turn27fetch0】.  
4. Docker-образ, легко поднимается и сохраняет данные.  
5. Есть готовый web UI и MCP-сервер для интеграции с AI-агентами【turn49fetch0】【turn55search3】.

**Apache AGE** как альтернатива, если:

- Уже есть сильная экспертиза в PostgreSQL.  
- Хотите унифицировать стек: SQL-БД + граф-слой внутри неё.  
- Важно переиспользовать существующие PostgreSQL-бэкапы и инструменты.

**Neo4j Community** как запасной вариант:

- Если уже есть опыт с Neo4j и не критично разделять инстансы по проектам.  
- Но придётся смириться с отсутствием multi-DB и управлением многими контейнерами.

---

### 7.2 Предлагаемая интеграция в HyperGraph

#### 7.2.1 Модель “1 project → 1 SQL DB + 1 Graph DB”

**С FalkorDB:**

- Один FalkorDB-инстанс (контейнер) на все проекты.  
- Внутри:
  - graph key = `project_id` (например, `graph_project_123`).  
- В PostgreSQL:
  - отдельная БД на проект (как у вас уже планируется).

**С Apache AGE:**

- PostgreSQL-инстанс на проект (или несколько проектов на инстанс, но разные БД).  
- В каждой БД – AGE-граф с именем `project_graph`.

**С Neo4j CE:**

- Neo4j-контейнер на проект.  
- PostgreSQL-БД на проект – отдельно.

#### 7.2.2 `switch(project_id)`

**FalkorDB:**

- В runtime сервис открывает соединение с FalkorDB.  
- Все запросы используют graph key = `project_id`.  
- “Переключение” проекта – это просто выбор другого graph key при формировании запроса.

**Apache AGE:**

- Соединение с конкретной PostgreSQL-БД (`project_id` → имя БД).  
- Внутри БД – граф с фиксированным именем (или тоже параметризованным).

**Neo4j CE:**

- Соединение с конкретным Neo4j-контейнером по host/port.  
- В конфиге хранить маппинг `project_id → neo4j_instance_url`.

#### 7.2.3 Хранение относительных путей

- В графе хранить **относительные пути** от корня проекта:
  - свойство `path` у узлов `File`, `Note`, `Task`.  
- Корень проекта хранить отдельно (в SQL-БД проекта или в конфиге сервиса).  
- При навигации:
  - по `project_id` определяем корень;
  - присоединяем относительный путь → полный путь для чтения файла.

---

## 8. Roadmap расширения

### 8.1 MVP (0–3 месяца)

1. **FalkorDB** в Docker Compose:
   - сервис `falkordb`;
   - volume для персистентности.  
2. Python-сервис HyperGraph:
   - `falkordb-py` для записи/чтения графа;
   - базовые Cypher-запросы:
     - исходящие/входящие ссылки;
     - broken/unresolved links;
     - traversal (до глубины 2–3).  
3. Web UI:
   - первый вариант – использовать FalkorDB Browser;
   - параллельно – минимальный UI на Cytoscape.js/vis-network.

### 8.2 Этап 2 (3–6 месяцев)

1. Добавить Apache AGE как альтернативный бэкенд:
   - поддержку двух “драйверов” графа (FalkorDB и AGE).  
2. Унифицировать SQL- и graph-слои:
   - общие схемы project_id, путей, метаданных.  
3. Улучшить UI:
   - фильтры по типам узлов, глубина traversal, поиск по путям.

### 8.3 Этап 3 (6+ месяцев)

1. При росте объёмов:
   - рассмотреть NebulaGraph для крупных инсталляций.  
2. Расширить граф-алгоритмы:
   - community detection, центральность, path analysis (через GDS или внешние библиотеки).  
3. Интеграция с LLM-агентами:
   - использовать FalkorDB MCP-сервер и LangChain/LlamaIndex интеграции【turn55search3】【turn51fetch0】.

---

## 9. Ссылки-источники

(официальные docs/репозитории/issue threads)

### FalkorDB

- FalkorDB GitHub【turn11fetch0】  
- Docker Hub `falkordb/falkordb`【turn64fetch0】  
- FalkorDB Docs: Clients (Python)【turn51fetch0】  
- FalkorDB Docs: Cypher support【turn55search0】【turn55search1】  
- FalkorDB Docs: MCP Server【turn55search3】  
- FalkorDB Docs: Browser/UI【turn49fetch0】  
- FalkorDB Blog: Multigraph Topology (multi-tenancy in OSS)【turn58fetch0】  
- FalkorDBLite: embedded Python graph DB【turn27fetch0】【turn30search0】  

### Apache AGE

- Apache AGE GitHub【turn0search10】  
- Apache AGE Overview【turn0search12】  
- Quick Start (Docker, Python)【turn21fetch0】【turn44fetch0】  
- Backup via pg_dump【turn22search10】  

### Neo4j

- Neo4j Docker docs & persistence【turn37fetch0】  
- Neo4j Python Driver Manual【turn43fetch0】  
- Neo4j Browser docs【turn56search3】  
- Multi-DB issue in Community Edition【turn8fetch0】  
- Backup/restore docs【turn22search0】【turn22search1】  

### Memgraph

- Memgraph GitHub【turn0search9】  
- Memgraph Docker & data durability【turn42fetch0】  
- Multi-tenancy docs【turn0search5】【turn0search6】  
- GQLAlchemy (Python OGM)【turn15search1】【turn15search3】  

### NebulaGraph

- NebulaGraph GitHub【turn3search9】  
- NebulaGraph docs: CREATE SPACE, graph spaces as isolated graphs【turn54find0】  
- Nebula Studio (Web GUI)【turn17fetch0】  
- Backup & Restore (BR) tool【turn22search16】  

### Kuzu

- Kuzu docs (embedded, Cypher, columnar storage)【turn61fetch0】  
- Kuzu Docker images (api-server, explorer)【turn26fetch0】  
- Kuzu Explorer (web UI)【turn59search1】  

### Other

- Dgraph GitHub & docs【turn2search7】【turn2search8】  
- OrientDB docs【turn3search10】【turn3search11】  
- Cytoscape.js【turn45search0】  
- Sigma.js【turn45search5】  
- vis-network【turn45search10】  

---

Если нужно, могу отдельно:

- расписать конкретный Cypher-дизайн схемы для Obsidian links MVP (узлы `Note`, `Link`, `BrokenLink`, отношения `LINKS_TO`, `RESOLVES_TO`);  
- предложить минимальный API-контракт для web-сервиса, который будет отдавать граф во фронтенд.