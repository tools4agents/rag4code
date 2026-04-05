# Дополненный анализ: Multi-model базы данных (SQL + Граф + Вектор)

## Краткий вывод

**Рекомендации:**

1. **ArcadeDB** — стратегический выбор для HyperGraph как единой multi-model платформы (SQL + граф + вектор + document + time-series).

2. **PostgreSQL + Apache AGE + pgvector** — тактический выбор, если команда уже глубоко вложилась в PostgreSQL-экосистему.

3. **FalkorDB** (из предыдущего анализа) остаётся лучшим выбором для MVP, если нужен именно граф без усложнения архитектуры.

---

## Сравнительная таблица (расширенная)

| Критерий | ArcadeDB | PostgreSQL + pgvector | PostgreSQL + Apache AGE + pgvector |
|----------|----------|----------------------|-----------------------------------|
| **Лицензия** | Apache 2.0 | PostgreSQL License | Apache 2.0 (AGE) + PostgreSQL License (pgvector) |
| **Multi-DB на сервере** | Да — несколько изолированных БД на одном сервере【turn3fetch0】 | Да — несколько БД на кластер | Да — несколько БД на кластер |
| **Docker + volumes** | Официальный образ, документированное монтирование【turn4find1】 | Множество готовых образов | Нужно собирать кастомный образ【turn7search2】 |
| **Python driver** | HTTP/JSON API + community drivers【turn8fetch0】 | Официальный psycopg2 + ORM | psycopg2 + apache-age-python |
| **Query language** | SQL, Cypher, Gremlin, GraphQL, MongoDB QL【turn1fetch1】 | SQL + vector type | SQL + openCypher (через cypher())【turn21fetch0】 |
| **Backup/restore** | Console/UI/HTTP API; копия директории БД【turn3fetch0】 | pg_dump / pg_restore | pg_dump / pg_restore |
| **Визуализация** | Studio (web UI), AI assistant (коммерческий)【turn3fetch0】 | pgAdmin и сторонние инструменты | Нет встроенного graph UI |
| **Риски/ограничения** | JVM-centric, молодой проект, экосистема меньше PostgreSQL | Нет встроенного graph слоя; граф через recursive CTE | Более сложный стек; AGE интеграция требует тестирования |

---

## Детальный анализ кандидатов

### 1. ArcadeDB

**Лицензия и open-source статус**
- Apache 2.0 — полностью open-source, "really FREE for any purpose"【turn4find1】
- Community Edition = Enterprise Edition по функциональности

**Multi-model архитектура**
ArcadeDB — настоящий multi-model DBMS, где движок изначально построен для поддержки всех моделей:
- Graph Database (native property graph)
- Document Database
- Key/Value
- Search Engine (full-text search)
- Time-Series
- Vector Embeddings (JVector engine)【turnturn1fetch1】
- Geospatial

**Ключевое отличие:** "Это не просто интерфейсы к движку, а сам движок построен для поддержки всех моделей. Это главное отличие от других multi-model DBMS, которые реализуют дополнительный слой API, имитирующий модели, но под капотом остаются одной моделью"【turn2find2】.

**Query Languages**
- SQL (для всех моделей)
- Open Cypher (для графов)
- Apache TinkerPop Gremlin (для графов)
- GraphQL
- MongoDB Query Language
- Redis commands【turn1fetch1】

**Multi-protocol доступ**
- HTTP/JSON API (native)
- PostgreSQL wire protocol (через плагин)
- MongoDB wire protocol
- Redis protocol【turn1fetch1】

**Multi-tenancy (изоляция проектов)**
- "Один сервер может хостить несколько изолированных БД, каждая БД изолирована и доступна по имени"【turn2find1】
- Studio UI позволяет создавать/удалять/бэкапить БД
- Настройки безопасности для multi-tenant deployments (например, `allowFileUrls` для LOAD CSV)【turn2find1】

**Vector Search (JVector)**
- Native JVector engine с DiskANN + HNSW hybrid
- SIMD acceleration
- Вектора хранятся прямо на узлах графа
- Поддержка similarity functions: COSINE, DOT_PRODUCT, EUCLIDEAN【turn6fetch0】

**GraphRAG примеры**【turn6fetch1】:
```sql
-- Семантический поиск по научным статьям
SELECT id, title, year
FROM Paper
ORDER BY vectorNeighbors('Paper[embedding]', [0.8, 0.2, 0.1, 0.1], 10) DESC
LIMIT 10;
```

```sql
-- GraphRAG hybrid: расширение векторных результатов через граф цитирований
SELECT topic.name AS topic, count(*) AS connections
FROM (
  MATCH {type: Paper, where: (id IN ['p2', 'p8', 'p4'])}
    .out('CITES'){as: cited}
    .out('COVERS'){as: topic}
  RETURN topic
)
GROUP BY topic
ORDER BY connections DESC
LIMIT 5;
```

**Docker + Persistence**【turn4find1】:
```bash
docker run --rm -p 2424:2424 -p 2480:2480 -p 5432:5432 \
  -v /path/on/host/databases:/home/arcadedb/databases \
  arcadedata/arcadedb:latest
```

**Python экосистема**【turn8fetch0】:
- HTTP/JSON API (можно через requests)
- Community drivers:
  - arcadedb-python-driver
  - pyarcade
  - arcadedb-python
  - arcadedb-embedded-python (embedded mode)

**Риски:**
- JVM-centric: основной API и экосистема Java-first
- Python drivers — community-driven, не такие зрелые как psycopg2
- Молодой проект, меньше production-опыта
- Меньше обучающих материалов и community

---

### 2. PostgreSQL + pgvector

**Лицензия**
- PostgreSQL License (open-source)
- pgvector: PostgreSQL License【turn5fetch0】

**Vector Search возможности**
- Vector similarity search для PostgreSQL
- Хранение векторов вместе с остальными данными
- Индексы: HNSW, IVFFlat
- ACID compliance, point-in-time recovery, JOINs【turn5fetch0】【turn0search6】

**Новые возможности pgvector 0.8.0**【turn5fetch1】:
- Улучшения для фильтрации (WHERE clause)
- Iterative index scans для предотвращения "overfiltering"
- Лучшее планирование запросов

**Docker:**
```bash
docker run -p 5432:5432 -e POSTGRES_PASSWORD=postgres \
  ankane/pgvector
```

**Python интеграция:**
- psycopg2 (официальный драйвер)
- SQLAlchemy, Django ORM
- LangChain, LlamaIndex интеграции

**Риски:**
- Нет встроенного graph layer
- Графовые запросы через recursive CTE — менее удобны чем Cypher
- Нет интегрированной GraphRAG логики

---

### 3. PostgreSQL + Apache AGE + pgvector

**Архитектура**
- PostgreSQL как основа
- Apache AGE — graph extension (openCypher поверх SQL)
- pgvector — vector similarity search

**Apache AGE особенности:**
- OpenCypher внутри PostgreSQL
- Граф хранится в PostgreSQL таблицах
- Наследует все преимущества PostgreSQL (ACID, транзакции, backup)

**Пример запроса**【turn21fetch0】:
```sql
SELECT create_graph('graph_name');

SELECT * FROM cypher('graph_name', $$
  MATCH (a:Person), (b:Person)
  WHERE a.name = 'Node A' AND b.name = 'Node B'
  CREATE (a)-[e:RELTYPE]->(b)
  RETURN e
$$) as (e agtype);
```

**Docker образ**【turn7search2】:
Нужно собирать кастомный образ с обоими расширениями:
```bash
git clone https://github.com/pgvector/pgvector.git
git clone https://github.com/apache/age.git
# Build custom image
```

**Python драйверы:**
- psycopg2
- apache-age-python (community)

**Риски:**
- Более сложный стек: PostgreSQL + AGE + pgvector
- Нет встроенного web UI для графов
- Graph queries через cypher() менее эргономичны чем в native graph DB
- AGE интеграция всё ещё развивается

---

## Как это влияет на HyperGraph архитектуру

### Сценарий 1: ArcadeDB как единая платформа

```
┌─────────────────────────────────────────────────────────┐
│                    HyperGraph Project                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │              ArcadeDB Database                   │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐        │   │
│  │  │   Graph  │ │ Document │ │  Vector  │        │   │
│  │  │  (Code,  │ │  (Docs,  │ │(Embeds)  │        │   │
│  │  │  Tasks)  │ │  ADR)    │ │          │        │   │
│  │  └──────────┘ └──────────┘ └──────────┘        │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐        │   │
│  │  │ Key/Val  │ │TimeSeries│ │  Search  │        │   │
│  │  │ (Cache)  │ │ (Metrics)│ │(FullText)│        │   │
│  │  └──────────┘ └──────────┘ └──────────┘        │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  Query Languages: SQL, Cypher, Gremlin, GraphQL        │
│  Protocols: HTTP, PostgreSQL, MongoDB, Redis           │
└─────────────────────────────────────────────────────────┘
```

**Преимущества для HyperGraph:**
1. **Единая база** для всех слоёв:
   - Code Layer → Graph vertices/edges
   - Knowledge Layer → Documents + vectors
   - Task Layer → Graph relationships
   - Memory Layer → Documents + time-series

2. **GraphRAG из коробки**:
   - Вектора на узлах графа
   - Hybrid queries (vector + graph traversal)
   - Semantic search + graph context

3. **Упрощение операций**:
   - Один backup для всех данных
   - Единая модель безопасности
   - Один мониторинг

### Сценарий 2: PostgreSQL как основа + расширения

```
┌─────────────────────────────────────────────────────────┐
│                    HyperGraph Project                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │           PostgreSQL Database                    │   │
│  │  ┌──────────────────┐ ┌──────────────────┐      │   │
│  │  │  Relational      │ │  Apache AGE      │      │   │
│  │  │  (SQL Tables)    │ │  (Graph via      │      │   │
│  │  │                  │ │   Cypher)        │      │   │
│  │  └──────────────────┘ └──────────────────┘      │   │
│  │  ┌──────────────────┐                           │   │
│  │  │  pgvector        │                           │   │
│  │  │  (Embeddings)    │                           │   │
│  │  └──────────────────┘                           │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  Query Languages: SQL + openCypher (via cypher())      │
│  Protocols: PostgreSQL                                 │
└─────────────────────────────────────────────────────────┘
```

**Преимущества:**
- Зрелая экосистема PostgreSQL
- Богатый инструментарий (pgAdmin, psql, ORMs)
- Глубокая интеграция с Python-стеком

**Недостатки:**
- Graph layer "bolted-on" через AGE
- Меньше интеграции между vector и graph
- Нет встроенного GraphRAG

---

## Сравнение для конкретных HyperGraph сценариев

### 1. Obsidian Links MVP

**ArcadeDB:**
- ✅ Cypher/SQL для графовых запросов
- ✅ Native graph traversal
- ⚠️ Избыточный для простого use case

**PostgreSQL + pgvector:**
- ✅ Простые SQL queries
- ⚠️ Graph traversal через recursive CTE
- ❌ Нет нативного graph layer

**PostgreSQL + AGE + pgvector:**
- ✅ Cypher через AGE
- ⚠️ Больше setup работы
- ⚠️ Меньше ergonomics чем native graph DB

### 2. Code Graph + Semantic Search

**ArcadeDB:**
- ✅ Graph + Vector в одном запросе
- ✅ JVector оптимизирован для graph workloads
- ✅ GraphRAG patterns из коробки

**PostgreSQL + pgvector:**
- ✅ Зрелый vector search
- ⚠️ Graph моделируется вручную
- ⚠️ Нет интеграции graph + vector

**PostgreSQL + AGE + pgvector:**
- ✅ И graph и vector в PostgreSQL
- ⚠️ Сложнее комбинировать в одном запросе
- ⚠️ Нет оптимизации для graph + vector join

### 3. Project-first Isolation

**ArcadeDB:**
- ✅ Multi-tenant architecture built-in【turn2find1】
- ✅ Каждая БД изолирована
- ✅ Studio UI для управления БД

**PostgreSQL:**
- ✅ Множество БД на кластер
- ✅ Role-based access control
- ⚠️ Нет специализированного multi-tenant UI

---

## Практические рекомендации

### Для MVP (0-6 месяцев)

**Выбор: FalkorDB** (из предыдущего анализа)

**Причины:**
- Проще начать
- Меньше moving parts
- Python-native
- Multi-tenancy из коробки

**Не выбирать ArcadeDB для MVP, потому что:**
- JVM-centric стек добавляет complexity
- Python drivers — community-driven
- Избыточный функционал для MVP

### Для этапа роста (6-18 месяцев)

**Добавить ArcadeDB** для специфичных workloads:

1. **GraphRAG для code search:**
   - Вектора эмбеддингов на узлах кода
   - Hybrid queries: semantic + structural

2. **Knowledge Graph для документации:**
   - Documents + vectors + relationships
   - Time-series для эволюции контента

**Архитектура:**
```
HyperGraph Services
    │
    ├── FalkorDB (Obsidian links, simple graph)
    │
    ├── ArcadeDB (GraphRAG, complex multi-model)
    │
    └── PostgreSQL (operational data, transactions)
```

### Для зрелой платформы (18+ месяцев)

**Консолидация на ArcadeDB** если:
- GraphRAG стал критичным
- Нужна tight интеграция graph + vector + time-series
- Команда готова к JVM-centric стеку

**Остаться на PostgreSQL stack** если:
- Реляционные данные доминируют
- Команда эксперты в PostgreSQL
- Нужна максимальная стабильность

---

## Миграционный путь

### Фаза 1: MVP (FalkorDB)

```yaml
services:
  hypergraph-graph:
    image: falkordb/falkordb:latest
    volumes:
      - falkordb_data:/data
    environment:
      - REDIS_ARGS=--save 60 1000
```

### Фаза 2: POC ArcadeDB

```yaml
services:
  hypergraph-arcadedb:
    image: arcadedata/arcadedb:latest
    ports:
      - "2480:2480"  # Studio UI
      - "2424:2424"  # HTTP API
      - "5432:5432"  # PostgreSQL protocol
    volumes:
      - arcadedb_data:/home/arcadedb/databases
    environment:
      - arcadedb.server.rootPassword=yourpassword
```

### Фаза 3: Hybrid Production

```yaml
services:
  # Для простых графов
  graph-simple:
    image: falkordb/falkordb:latest
    
  # Для GraphRAG workloads  
  graph-rag:
    image: arcadedata/arcadedb:latest
    
  # Для транзакционных данных
  postgres:
    image: postgres:16
    # + pgvector extension
```

---

## Итоговая матрица решений

| Критерий | FalkorDB | ArcadeDB | PostgreSQL + AGE + pgvector |
|----------|----------|----------|----------------------------|
| **MVP скорость** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **GraphRAG готовность** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| **Python ergonomics** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Multi-model** | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Production maturity** | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Community size** | ⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Learning curve** | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |

**Рекомендация:**
1. **MVP** → FalkorDB
2. **GraphRAG POC** → ArcadeDB
3. **Production** → Hybrid (FalkorDB + ArcadeDB + PostgreSQL)

---

## Ссылки-источники

### ArcadeDB
- Официальная документация: https://docs.arcadedb.com【turn1fetch1】
- GitHub репозиторий: https://github.com/ArcadeData/arcadedb【turn1fetch0】
- Multi-tenancy документация【turn2find1】
- Docker и persistence【turn4find1】

### PostgreSQL + pgvector
- pgvector GitHub: https://github.com/pgvector/pgvector【turn5fetch0】
- Release notes 0.8.0【turn5fetch1】

### PostgreSQL + Apache AGE
- Документация Apache AGE【turn21fetch0】
- Docker setup для AGE + pgvector【turn7search2】
