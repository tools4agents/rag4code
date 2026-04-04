**ArcadeDB** — это современная **open-source мультимодельная база данных**, которая объединяет несколько типов хранения данных в одном движке (graph, document, key-value, vector, time-series и др.). Она создавалась как **эволюция/форк OrientDB**, но с полностью переработанным ядром и упором на производительность и простоту эксплуатации. ([GitHub][1])

Ниже — подробный разбор архитектуры, возможностей и особенностей.

---

# 1. Общая идея ArcadeDB

Главная концепция — **True Multi-Model Database**.

Это означает, что разные модели данных поддерживаются **нативно в одном движке**, а не через плагины или отдельные системы. ([ArcadeDB][2])

То есть вместо архитектуры:

```
Neo4j (graph)
+ MongoDB (documents)
+ Elasticsearch (search)
+ Redis (key-value)
+ vector DB
```

можно использовать:

```
ArcadeDB
```

Это уменьшает:

* сложность инфраструктуры
* ETL между системами
* задержки
* расходы на эксплуатацию. ([FitGap][3])

---

# 2. Поддерживаемые модели данных

ArcadeDB поддерживает несколько типов данных **в одном хранилище**:

### 1️⃣ Graph database

Поддержка графовой модели:

* вершины (vertices)
* рёбра (edges)
* traversal

Поддерживаемые языки:

* Cypher (как в Neo4j)
* Gremlin

Это удобно для:

* knowledge graphs
* recommendation systems
* fraud detection
* social networks.

---

### 2️⃣ Document database

Документы JSON-типа (аналог MongoDB).

Особенности:

* гибкая схема
* вложенные структуры
* индексы

Используется для:

* веб-приложений
* микросервисов
* хранения событий.

---

### 3️⃣ Key-Value store

ArcadeDB может работать как **Redis-подобное хранилище**.

Поддерживается Redis-driver. ([GitHub][1])

Используется для:

* кэшей
* сессий
* быстрых lookup-операций.

---

### 4️⃣ Vector database

Поддержка **vector embeddings** (для AI).

Используется для:

* semantic search
* RAG
* recommendation systems
* similarity search.

---

### 5️⃣ Time-Series

Хранение временных рядов:

* метрики
* telemetry
* IoT данные.

Поддерживается **PromQL-style querying**. ([ArcadeDB][2])

---

### 6️⃣ Full-text search

Встроенный search engine:

* full-text индексы
* поиск по тексту.

---

# 3. Мультиязыковые запросы

ArcadeDB поддерживает **несколько языков запросов одновременно**.

Можно использовать любой из них:

* SQL
* Cypher
* Gremlin
* GraphQL
* MongoDB query language
* Java API. ([ArcadeDB][2])

Например один и тот же запрос:

SQL

```sql
SELECT FROM Person
WHERE age > 25
```

Cypher

```cypher
MATCH (p:Person)
WHERE p.age > 25
RETURN p
```

Это удобно при миграциях.

---

# 4. Архитектура и производительность

ArcadeDB написан на **Java (Low Level Java)** и использует техники *mechanical sympathy* для высокой производительности. ([GitHub][1])

Особенности:

### High performance engine

* миллионы записей в секунду
* traversal скорость не зависит от размера графа

### Low GC pressure

* оптимизированная работа с памятью

### Малый footprint

* может работать даже на **Raspberry Pi**.

---

# 5. ACID и транзакции

ArcadeDB — **полностью транзакционная база данных**.

Поддерживает:

* ACID transactions
* Write-Ahead Log (WAL)
* rollback после crash. ([ArcadeDB][4])

Это позволяет использовать её в production-системах.

---

# 6. Кластеризация и отказоустойчивость

Для распределённых систем есть:

### Raft consensus

Используется алгоритм **Raft** для согласованности между нодами. ([ArcadeDB][4])

Это даёт:

* replication
* fault tolerance
* leader election.

---

# 7. Способы использования

ArcadeDB можно использовать в нескольких режимах.

### Embedded database

База работает **внутри приложения**.

Пример:

```
Java app
 + ArcadeDB embedded
```

Это похоже на:

* SQLite
* DuckDB.

---

### Client-Server

Запуск как полноценный DB сервер.

Подключение через:

* HTTP/JSON
* Postgres protocol
* Redis protocol
* MongoDB driver. ([Ted Neward's Research][5])

Это удобно для интеграции с существующими инструментами.

---

# 8. Совместимость с другими системами

ArcadeDB специально сделан так, чтобы миграции были простыми.

Поддерживается:

* Neo4j drivers
* MongoDB drivers
* Redis drivers
* Postgres wire protocol. ([Ted Neward's Research][5])

Также можно мигрировать из:

* OrientDB
* Neo4j.

---

# 9. Graph algorithms

ArcadeDB содержит **встроенные алгоритмы графов**.

Примеры:

* shortest path
* centrality
* clustering

Всего около **60+ алгоритмов**. ([ArcadeDB][2])

Это важно для:

* графовой аналитики
* knowledge graph.

---

# 10. Open Source модель

ArcadeDB распространяется под лицензией:

**Apache 2.0**

Это означает:

* полностью open source
* нет enterprise edition
* все функции доступны бесплатно. ([ArcadeDB][2])

---

# 11. Основные преимущества

### 1️⃣ Один движок для всех моделей

Уменьшает complexity архитектуры.

---

### 2️⃣ Высокая производительность

Оптимизированный Java-движок.

---

### 3️⃣ Много языков запросов

SQL + Cypher + Gremlin + GraphQL.

---

### 4️⃣ Embedded + distributed

Можно использовать:

* как SQLite
* как distributed DB.

---

### 5️⃣ Хорошо подходит для AI-систем

Потому что есть:

* graph
* vector search
* documents.

---

# 12. Когда ArcadeDB особенно полезен

Он хорошо подходит для систем где нужно **несколько типов данных одновременно**.

Типичные кейсы:

### Knowledge graph

AI + semantic relationships.

---

### Recommendation systems

Graph + embeddings.

---

### Fraud detection

Graph traversal + analytics.

---

### AI agents / RAG systems

* vector embeddings
* graph memory
* structured data.


✅ **Коротко:**
ArcadeDB — это **high-performance multi-model database**, объединяющая graph, document, vector и другие типы данных в одном движке с поддержкой нескольких языков запросов.

---

💡 Если хочешь, могу ещё разобрать:

* архитектуру **ArcadeDB storage engine (очень интересная)**
* сравнение **ArcadeDB vs Neo4j vs ArangoDB vs SurrealDB**
* как ArcadeDB используют в **AI / knowledge graph / RAG системах**.

[1]: https://github.com/ArcadeData/arcadedb?utm_source=chatgpt.com "GitHub - ArcadeData/arcadedb: ArcadeDB Multi-Model Database, one DBMS that supports SQL, Cypher, Gremlin, HTTP/JSON, MongoDB and Redis. ArcadeDB is a conceptual fork of OrientDB, the first Multi-Model DBMS. ArcadeDB supports Vector Embeddings."
[2]: https://arcadedb.com/?utm_source=chatgpt.com "ArcadeDB - The Next Generation Multi-Model Database | Graph, Document, Key-Value, Vector & Time-Series"
[3]: https://us.fitgap.com/products/arcadedb?utm_source=chatgpt.com "ArcadeDB reviews 2026 | FitGap"
[4]: https://arcadedb.com/index.html?utm_source=chatgpt.com "ArcadeDB - The Next Generation Multi-Model Database | Graph, Document, Key-Value, Vector & Time-Series"
[5]: https://research.tedneward.com/storage/arcadedb/index.html?utm_source=chatgpt.com "ArcadeDB"

Да — **в этом и есть одна из главных идей мультимодельных БД вроде ArcadeDB**.
В них **можно комбинировать разные модели данных (graph, document, vector и т.д.) внутри одного запроса или цепочки запросов**. Причём это делается **без ETL между системами**, потому что все модели хранятся в одном движке. ([ArcadeDB][1])

Разберём подробнее, **как именно это работает**.

---

# 1. Комбинирование разных моделей в одном запросе

ArcadeDB хранит:

* графовые сущности (vertices / edges)
* документы
* embeddings
* key-value
* time-series

**в одном storage engine**. Поэтому запрос может:

1. выбрать документы
2. пройти по графу
3. сделать vector similarity
4. применить фильтры

— всё это в одном pipeline. ([ArcadeDB][1])

---

# 2. Пример: документ + граф

Представим систему знаний:

```
Document
 - id
 - text
 - embedding

Author (vertex)

Edge: WROTE
```

Запрос может быть таким:

1️⃣ найти документы по текстовому фильтру
2️⃣ перейти к авторам
3️⃣ найти их коллег

Пример (условный SQL / graph traversal):

```sql
SELECT expand(out('WROTE'))
FROM (
  SELECT FROM Document
  WHERE category = 'AI'
)
```

Что происходит:

1. фильтр по **document model**
2. затем **graph traversal**

---

# 3. Пример: vector search + graph

Это популярный сценарий **RAG / knowledge graph**.

Шаги запроса:

1. найти **семантически похожие документы** (vector search)
2. пройти по графу связей
3. отфильтровать по метаданным

ArcadeDB прямо описывает этот сценарий:

* vector similarity ищет похожие документы
* затем результаты обогащаются **graph traversal**
* можно фильтровать по автору, департаменту и т.д. ([ArcadeDB][2])

Пример логики:

```
vector search -> documents
      ↓
graph traversal -> related entities
      ↓
filters -> permissions / metadata
```

---

# 4. Пример: recommendation system

ArcadeDB показывает такой гибридный запрос:

```
graph traversal (users with similar behaviour)
+
vector similarity (similar products)
+
ranking
```

Это позволяет одновременно использовать:

* collaborative filtering (graph)
* content-based filtering (vectors) ([ArcadeDB][3])

---

# 5. Можно ли смешивать разные query languages?

Есть два варианта.

### 1️⃣ Один язык

Чаще всего используют **SQL-подобный язык** ArcadeDB.

Он уже поддерживает:

* graph traversal
* document filtering
* join-подобные операции.

---

### 2️⃣ Разные API / драйверы

ArcadeDB поддерживает:

* SQL
* Cypher
* Gremlin
* GraphQL
* MongoDB query language ([GitHub][4])

Можно делать так:

```
MongoDB query → получить документы
Cypher query → пройти по графу
```

Но чаще используют **единый язык внутри транзакции**.

---

# 6. Комбинирование в серии запросов (pipeline)

Часто используется паттерн:

```
Query 1 → document filter
Query 2 → graph traversal
Query 3 → vector similarity
Query 4 → aggregation
```

Все запросы выполняются **в одной транзакции**.

---

# 7. Почему это возможно

В ArcadeDB:

* graph vertices — это фактически **расширенные документы**
* edges — тоже **документы**

Поэтому разные модели **не изолированы**.

Например:

```
Vertex
{
  name: "Alice",
  department: "AI",
  embedding: [...]
}
```

Один объект может одновременно быть:

* графовой вершиной
* JSON-документом
* иметь embedding.

---

# 8. Типичные гибридные сценарии

Вот реальные use-cases:

### Knowledge Graph + Semantic Search

```
vector search → graph traversal → ranking
```

---

### Fraud Detection

```
transaction filter → graph neighborhood → anomaly scoring
```

---

### Recommendation Systems

```
user similarity graph → product embeddings
```

---

### RAG systems

```
embedding search → graph context → document retrieval
```

---

# 9. Ограничение, которое важно понимать

Хотя модели комбинируются, **обычно есть один основной язык запроса**.

Например:

* SQL с graph traversal
* Cypher с property filters

Не всегда можно буквально написать:

```
Cypher + Mongo query + Gremlin
```

в одной строке.

Но **логически операции смешиваются**.

---

✅ **Короткий ответ:**
Да — в ArcadeDB можно комбинировать фильтры и операции разных моделей (graph, document, vector и др.) в одном запросе или в одном pipeline запросов, потому что все модели хранятся нативно в одном движке. ([ArcadeDB][1])

---

💡 Если интересно, могу ещё показать:

* **реальный пример сложного hybrid-query в ArcadeDB (graph + vector + metadata)**
* или сравнить **ArcadeDB vs ArangoDB vs SurrealDB по мультимодельным запросам** — там есть очень интересные архитектурные различия.

[1]: https://arcadedb.com/?utm_source=chatgpt.com "ArcadeDB - The Next Generation Multi-Model Database | Graph, Document, Key-Value, Vector & Time-Series"
[2]: https://arcadedb.com/knowledge-graphs.html?utm_source=chatgpt.com "Knowledge Graphs & Semantic Search with ArcadeDB | AI-Powered Knowledge Management"
[3]: https://arcadedb.com/recommendation-engine.html?utm_source=chatgpt.com "Intelligent Recommendation Engines with ArcadeDB | Graph + Vector Database"
[4]: https://github.com/ArcadeData/arcadedb?utm_source=chatgpt.com "GitHub - ArcadeData/arcadedb: ArcadeDB Multi-Model Database, one DBMS that supports SQL, Cypher, Gremlin, HTTP/JSON, MongoDB and Redis. ArcadeDB is a conceptual fork of OrientDB, the first Multi-Model DBMS. ArcadeDB supports Vector Embeddings."
