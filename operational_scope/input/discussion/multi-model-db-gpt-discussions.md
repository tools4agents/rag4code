Давай обсудим мульти модельные БД для этого проекта. Я присматривался к ArcadeDB.

Да, я заметил твою склонность к “multi” 😄
И в твоем случае она очень логична архитектурно.

Твой проект действительно хорошо ложится именно на multi-model DB, потому что у тебя одновременно есть:

* graph relationships
* document storage
* full-text search
* metadata
* embeddings/vector search (в будущем почти наверняка)
* potentially event logs
* filesystem indexing state

То есть это уже не “просто graph DB”.

---

# Что тебе реально нужно от БД

Для твоего Markdown Graph MCP я бы выделил такие требования:

| Требование               | Важность      |
| ------------------------ | ------------- |
| Native graph traversal   | Очень высокая |
| Document model           | Очень высокая |
| Embedded metadata        | Высокая       |
| Fast link traversal      | Очень высокая |
| Full-text search         | Высокая       |
| Vector search            | Желательно    |
| Open source license      | Критично      |
| Embeddable/self-hosted   | Критично      |
| MCP/AI friendly          | Высокая       |
| Simple deployment        | Желательно    |
| Transaction support      | Очень важно   |
| Rust/Java ecosystem      | Бонус         |
| Stable long-term license | КРИТИЧНО      |

И вот тут начинается самое интересное.

---

# Главная проблема рынка сейчас

Многие DB vendors начали:

* relicensing
* BSL
* SSPL
* source-available
* open-core

После:

* MongoDB
* Redis
* Elastic
* Terraform
* Cockroach
* Neo4j ecosystem

люди стали очень осторожны.

И ты правильно на это смотришь заранее.

---

# Мой общий вывод для твоего проекта

## Лучшие кандидаты:

| DB                      | Моя оценка |
| ----------------------- | ---------- |
| ArcadeDB                | ⭐⭐⭐⭐⭐      |
| ArangoDB                | ⭐⭐⭐⭐       |
| SurrealDB               | ⭐⭐⭐⭐       |
| PostgreSQL + extensions | ⭐⭐⭐⭐⭐      |
| Neo4j                   | ⭐⭐         |
| OrientDB                | ⭐⭐⭐        |
| TerminusDB              | ⭐⭐⭐        |
| HugeGraph               | ⭐⭐⭐        |
| Memgraph                | ⭐⭐         |

---

# 1. ArcadeDB

## Очень сильный кандидат для тебя

---

## Что это такое

ArcadeDB:

* graph
* document
* key-value
* vector
* time-series
* full-text

в одном движке. ([ArcadeDB][1])

---

## Самое важное

# Apache 2.0

И они ПУБЛИЧНО обещают:

> license never changes

([ArcadeDB][1])

Это сейчас редкость.

---

## Почему он особенно хорош для твоего проекта

### 1. Native graph

Тебе нужны:

```text
incoming_links
outgoing_links
neighbors
traversals
orphans
dependency_graph
```

ArcadeDB очень хорошо под это подходит.

---

### 2. Multi-model реально нативный

Не “graph поверх JSON”.

А именно:

* documents
* graph edges
* vectors
* search

в одном storage engine. ([ArcadeDB][1])

---

### 3. Хорошо ложится на Markdown Graph Runtime

Ты можешь хранить:

```text
Vertex:
  markdown_file

Edges:
  LINKS_TO
  EMBEDS
  TAGGED_BY
  ALIASES
  REFERENCES_TERM
```

И одновременно:

* metadata
* AST cache
* embeddings
* filesystem state

---

### 4. SQL + Cypher + Gremlin

Это очень удобно.

ИИ агентам можно давать:

* Cypher-like traversal
* SQL metadata querying

---

## Минусы

### 1. JVM

Это Java ecosystem.

Если хочешь ultra-light Rust-native stack — может не зайти.

---

### 2. Молодая экосистема

Не такой mature как PostgreSQL.

---

### 3. Smaller community

Но для infra-tooling это не всегда проблема.

---

# 2. ArangoDB

Раньше был одним из лучших вариантов.

Но сейчас:

# BSL

и это большая проблема для многих OSS проектов. ([ArcadeDB][1])

---

## Технически

Очень хорош:

* graph
* documents
* search
* mature clustering
* AQL отличный язык

---

## Но лицензия…

Если ты хочешь:

# strong OSS ideology

то ArangoDB сейчас менее привлекателен.

---

# 3. SurrealDB

Очень интересный.

---

## Плюсы

### 1. AI-native vibe

Очень чувствуется что они думают:

* graph
* realtime
* agents
* relationships
* records as graph

---

### 2. Rust ecosystem

Это большой плюс.

---

### 3. Очень приятная модель данных

Почти идеально для:

* knowledge systems
* semantic graphs
* agent memory

---

### 4. Graph + document очень elegant

---

## Но…

# BSL 1.1

([SurrealDB][2])

---

## Их BSL довольно permissive

Они разрешают:

* embedding
* SaaS
* production use

Запрещают только:

* competing DBaaS

([SurrealDB][2])

---

## Но это все равно НЕ open source по OSI

Это важно понимать.

---

## Еще момент

SurrealDB пока:

* очень быстро развивается
* иногда нестабилен
* архитектура еще “движется”

В 2025–2026 они активно переписывали core architecture. ([Reddit][3])

---

# 4. PostgreSQL + extensions

Вот неожиданный кандидат.

---

# Очень underrated вариант

Например:

* PostgreSQL
* pgvector
* Apache AGE
* recursive CTE
* JSONB
* trigram/fulltext

---

## Почему это может быть лучшим pragmatic choice

### 1. Самая стабильная лицензия в мире

# PostgreSQL License

Практически MIT-style.

---

### 2. Maximum ecosystem stability

Через 15 лет PostgreSQL все еще будет жить.

---

### 3. Очень mature tooling

---

### 4. Ты можешь хранить:

```text
documents
edges
embeddings
metadata
events
```

в одной системе.

---

## Но

Graph traversal менее elegant.

---

# 5. Neo4j

Я бы не советовал.

Причины:

* licensing ambiguity/history
* enterprise gating
* ecosystem drift
* not really multi-model

---

# 6. OrientDB

Интересный исторический вариант.

Кстати:

# ArcadeDB создал бывший создатель OrientDB

И ArcadeDB во многом:

* spiritual successor
* cleaner redesign

---

# Очень важный architectural вопрос

## Нужен ли тебе вообще отдельный graph DB?

Вот это реально важный вопрос.

Потому что твой workload:

* bounded
* local-first
* repo-scoped
* not internet-scale

---

# Возможно тебе лучше:

## SQLite/Postgres + graph layer

Например:

```text
documents
links
aliases
terms
embeddings
```

через relational model.

---

# Но есть нюанс

Ты хочешь:

# semantic infrastructure runtime

а не просто storage.

И тут graph-native DB начинает выигрывать.

---

# Мой честный architectural вывод

## Если смотреть именно под твой use case

---

# Лучший ideological fit

## ArcadeDB

Потому что:

* Apache 2.0
* multi-model
* graph-native
* AI/knowledge friendly
* no enterprise lock
* no relicensing fears
* strong fit for document graph runtime

---

# Лучший pragmatic fit

## PostgreSQL

Потому что:

* ecosystem
* stability
* boring technology
* universal deployment
* infinite tooling

---

# Самый "future AI-native"

## SurrealDB

Но:

* license risk
* maturity risk
* architectural churn

---

# Что бы я сделал на твоем месте

## MVP

Вообще начал бы с:

# SQLite/Postgres abstraction layer

и abstraction interfaces:

```ts
GraphStore
DocumentStore
VectorStore
ReferenceIndex
```

---

Потом сделал бы adapters:

* Postgres adapter
* ArcadeDB adapter
* SurrealDB adapter

---

# Почему это важно

Потому что:

# database lock-in убивает infra projects

---

# И еще одна важная мысль

Твой проект очень похож не на "database app".

А на:

# compiler/runtime/indexing infrastructure

Поэтому storage abstraction тут очень важен.

---

# Мой личный топ для твоего проекта

| DB         | Recommendation                  |
| ---------- | ------------------------------- |
| ArcadeDB   | Лучший баланс                   |
| PostgreSQL | Самый безопасный                |
| SurrealDB  | Самый visionary                 |
| ArangoDB   | Хорош технически, хуже лицензия |
| Neo4j      | Не советую                      |
| SQLite     | Отличный MVP вариант            |

---

И да, твоя идея очень хорошо ложится на концепцию:

# "Knowledge Graph Infrastructure for AI agents"

а это уже намного больше чем просто markdown link updater.

[1]: https://arcadedb.com/index.html?utm_source=chatgpt.com "ArcadeDB: Open-Source Multi-Model Graph Database"
[2]: https://surrealdb.com/license?utm_source=chatgpt.com "License FAQs | SurrealDB"
[3]: https://www.reddit.com/r/surrealdb/comments/1r78b1j/introducing_surrealdb_30/?utm_source=chatgpt.com "Introducing SurrealDB 3.0"


Моя экосистема вообще python ) В целом меня устроит сервис БД который можно поднять в docker контейнере и чтобы мой сервис просто мог отправлять ему запросы) Да абстракции у меня будут. Но пока в качестве BD возьму ArcadeDB.