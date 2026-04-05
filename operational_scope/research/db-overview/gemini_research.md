# **Архитектура и выбор графовой базы данных для HyperGraph: Исследование решений с изоляцией на уровне проектов**

Развитие современных систем управления знаниями привело к необходимости создания сложных структур, способных описывать не только иерархические зависимости, но и многомерные связи между документацией, исходным кодом и рабочими процессами. Проект HyperGraph нацелен на создание единого графа знаний, где источником истины выступают файлы, хранящиеся в Git-репозиториях, а оперативным хранилищем — проекции в виде реляционных и графовых баз данных. Ключевой особенностью системы является модель «Project-first», требующая строгой изоляции данных между различными проектами. В данном отчете проводится детальный анализ опенсорсных графовых решений, способных обеспечить такую изоляцию, персистентность в Docker-контейнерах и возможность интеграции с современными инструментами визуализации.

## **Концепция гиперграфа знаний в модели Project-first**

Видение HyperGraph предполагает объединение трех фундаментальных слоев информации: графа документации (преимущественно Markdown), графа кода (результаты статического анализа и данные LSP) и слоя памяти рабочих процессов. В рамках модели «Project-first» проект определяется как путь к директории с единственным корнем Git. Это накладывает специфические требования на архитектуру хранения: каждый проект должен иметь собственную изолированную базу данных. Такая изоляция необходима не только для обеспечения безопасности и предотвращения утечек данных между проектами, но и для упрощения процедур резервного копирования, восстановления и миграции.  
Графовая проекция в этой архитектуре служит для выполнения сложных запросов обхода (traversal), поиска кратчайших путей и анализа связности, которые затруднительны в традиционных реляционных СУБД.1 При этом реляционная СУБД (PostgreSQL) сохраняет роль хранилища оперативного состояния, создавая связку «1 проект → 1 SQL DB \+ 1 Graph DB».

## **Анализ ландшафта Open Source графовых СУБД**

Рынок графовых систем управления данными в 2024–2025 годах предлагает широкий спектр решений, однако многие из них имеют существенные ограничения в своих бесплатных редакциях, особенно в вопросах мультиарендности и создания нескольких баз данных внутри одного экземпляра.1

### **Neo4j Community Edition: Стандарт индустрии и его ограничения**

Neo4j остается наиболее популярной графовой СУБД, предлагающей зрелую экосистему и мощный язык запросов Cypher.1 Однако Community Edition (CE) обладает критическим ограничением для проекта HyperGraph: она не поддерживает работу с несколькими базами данных внутри одного процесса.6 В версии CE доступна только одна пользовательская база данных и системная база данных.6  
Для реализации изоляции проектов в Neo4j CE существует два основных пути. Первый — запуск отдельного Docker-контейнера для каждого проекта. Этот подход обеспечивает физическую изоляцию, но крайне неэффективен с точки зрения ресурсов (CPU и RAM) при наличии десятков проектов.8 Второй путь — использование логической изоляции через метки узлов (labels), например, добавление префикса ProjectA\_ ко всем типам узлов и ребер.8 Это усложняет написание запросов и не дает гарантий безопасности на уровне СУБД. Кроме того, такие функции, как управление ролями и расширенное управление пользователями, также ограничены в версии CE.7 Тем не менее, Neo4j обладает лучшей документацией и поддержкой сообщества, а её лимиты на размер графа в последних версиях практически сняты (до 34 миллиардов узлов и связей), что делает её пригодной для крупных одиночных проектов.9

### **Memgraph: Высокопроизводительный In-memory граф**

Memgraph позиционируется как альтернатива Neo4j, написанная на C++ и оптимизированная для работы в оперативной памяти, что обеспечивает сверхнизкие задержки.3 Она полностью совместима с протоколом Bolt и языком Cypher.11  
В контексте HyperGraph Memgraph привлекателен поддержкой пользовательских модулей на Python (MAGE), что позволяет встраивать логику анализа непосредственно в процесс обработки графа.11 Однако, как и в случае с Neo4j, функция многопользовательской аренды (multi-tenancy), позволяющая создавать изолированные базы данных внутри одного инстанса, доступна только в Enterprise-версии.13 В Enterprise-редакции можно создавать именованные базы данных и переключаться между ними с помощью команды USE DATABASE, но в открытой версии пользователю придется управлять множеством инстансов или использовать логическое разделение данных.14

### **Apache AGE: Графовое расширение для PostgreSQL**

Apache AGE представляет собой расширение для PostgreSQL, которое добавляет поддержку графовой модели данных (Labeled Property Graph) непосредственно в реляционную базу.2 Это решение выглядит наиболее перспективным для HyperGraph, так как позволяет хранить SQL-состояние и графовую проекцию внутри одной СУБД PostgreSQL.2  
AGE поддерживает стандарт OpenCypher, интегрируя его в SQL-запросы через функцию cypher().17 Изоляция проектов здесь реализуется естественным образом: поскольку каждый проект HyperGraph имеет свою БД в Postgres, включение расширения AGE в этой базе создает изолированную графовую среду.20 AGE использует собственные пространства имен (namespaces) для хранения таблиц узлов и ребер, что предотвращает конфликты с существующими реляционными данными.2 Основным преимуществом является возможность выполнения гибридных запросов, объединяющих мощь SQL (для фильтрации и агрегации) и Cypher (для обхода графа).17

| Параметр | Neo4j Community | Memgraph (OSS) | Apache AGE |
| :---- | :---- | :---- | :---- |
| **Лицензия** | GPL v3 | BSL / OSS | Apache 2.0 |
| **Мульти-БД (в одном инстансе)** | Нет | Нет (Enterprise) | Да (через Postgres) |
| **Режим хранения** | On-disk (WAL) | In-memory \+ Snapshot | On-disk (Postgres) |
| **Язык запросов** | Cypher | Cypher | Cypher \+ SQL |
| **Python SDK** | Отличный | Совместим с Neo4j | Через Postgres драйвер |

### **Kùzu: Встраиваемая OLAP-система для Python**

Kùzu — это встраиваемая (embedded) графовая СУБД, написанная на C++, которая не требует запуска отдельного сервера.23 Она работает аналогично DuckDB или SQLite: библиотека подключается непосредственно к Python-процессу и работает с файлами базы данных на диске.23  
Для модели HyperGraph это идеальный кандидат с точки зрения изоляции. Каждый проект может хранить свою графовую базу в поддиректории .git или специальной папке проекта. Подключение выполняется просто: db \= kuzu.Database('./project\_db').25 Kùzu оптимизирована для аналитических нагрузок (OLAP), используя векторизованное исполнение запросов и современные алгоритмы соединений (worst-case optimal joins), что делает её значительно быстрее Neo4j на задачах многошагового обхода графа.12 Она поддерживает OpenCypher и транзакции ACID.23

### **FalkorDB: Низкие задержки и разреженные матрицы**

FalkorDB (преемник RedisGraph) использует математический аппарат разреженных матриц для представления графа и линейную алгебру для выполнения запросов.28 Она работает как модуль Redis, что обеспечивает высокую скорость обработки данных.28  
Уникальной особенностью FalkorDB в контексте данного исследования является поддержка нескольких графов (multi-graph) в рамках одного инстанса даже в открытой версии.31 Разработчики FalkorDB активно продвигают паттерн "Per-User Graph Isolation", где каждый пользователь или проект получает выделенный именованный граф (например, project\_1, project\_2), что исключает риск утечки данных и сохраняет стабильную производительность при масштабировании до тысяч проектов.33 Кроме того, FalkorDB обладает встроенной поддержкой векторных индексов, что критично для задач GraphRAG (Retrieval-Augmented Generation).30

## **Механизмы изоляции данных без Enterprise-лицензий**

Обеспечение изоляции на уровне проекта является центральной проблемой при использовании опенсорсных версий графовых СУБД. Исследование показывает, что стратегии изоляции можно разделить на три архитектурных паттерна.

### **Паттерн 1: База данных как файл (Kùzu)**

Этот подход обеспечивает максимально полную физическую изоляцию. База данных проекта — это набор файлов в файловой системе хоста или внутри Docker-тома.27

* **Преимущества:** Нулевые затраты на управление сервером; простая миграция (копирование папки); естественное соответствие структуре проекта.  
* **Риски:** Невозможность одновременного доступа к базе из нескольких процессов в режиме записи (только многопоточность внутри одного процесса).38

### **Паттерн 2: Граф внутри реляционной схемы (Apache AGE)**

Использование PostgreSQL как фундамента позволяет изолировать графы на уровне баз данных или схем.13

* **Преимущества:** Единый жизненный цикл с основным хранилищем проекта; использование зрелых механизмов бэкапа Postgres (pg\_dump).39  
* **Риски:** Необходимость управления расширениями и специфическими типами данных Postgres.

### **Паттерн 3: Именованные графы в общей памяти (FalkorDB)**

Хранение множества графов в одном процессе СУБД с логическим разделением по ключам/именам.31

* **Преимущества:** Высокая плотность упаковки проектов на одном сервере; минимальные накладные расходы на переключение контекста.  
* **Риски:** Общая оперативная память — один тяжелый запрос в одном проекте может замедлить работу всех остальных.13

## **Управление состоянием и персистентность в Docker-окружениях**

Для надежной работы HyperGraph в Docker необходимо обеспечить сохранение данных при перезагрузке контейнеров. Все рассмотренные кандидаты поддерживают монтирование внешних томов (volumes).1

### **Сохранение данных и Docker Volumes**

Стандартная практика для Docker заключается в использовании именованных томов или bind-mounts. Например, для FalkorDB данные сохраняются в /var/lib/falkordb/data, и при запуске контейнера с флагом \-v falkordb\_data:/var/lib/falkordb/data состояние будет восстановлено после выключения ПК.43 Аналогично, Neo4j использует директорию /data.44 В случае Kùzu, контейнеру приложения просто передается доступ к папке с проектами, где лежат файлы БД.25

### **Стратегии Backup/Restore**

Процедура резервного копирования критически важна для MVP.

1. **Apache AGE:** Используется стандартный pg\_dump, который создает SQL-скрипт с определениями графов, узлов и ребер.39 Это самый надежный способ, гарантирующий консистентность.47  
2. **Kùzu:** Резервное копирование заключается в создании снимка файловой директории. Существуют сторонние решения, такие как Litestream, которые могут обеспечивать непрерывное реплицирование таких баз в облачное хранилище.48  
3. **FalkorDB:** Поддерживает механизмы RDB (снимки) и AOF (лог операций) Redis.43 Для бэкапа достаточно сохранить файл dump.rdb.

| СУБД | Механизм Backup | Сложность восстановления |
| :---- | :---- | :---- |
| **Neo4j CE** | Копирование папки /data | Низкая (требует остановки) |
| **Apache AGE** | pg\_dump | Средняя (стандарт SQL) |
| **Kùzu** | Файловое копирование | Очень низкая |
| **FalkorDB** | Redis RDB / Snapshot | Низкая |

## **Интеграция с Core-сервисами: Python SDK и паттерны индексации**

Core-сервисы HyperGraph должны иметь возможность эффективно писать и читать данные. Все выбранные СУБД имеют качественные Python-драйверы.19

### **Паттерны массовой загрузки (Bulk Upsert)**

Для первичной индексации Obsidian-заметок или репозитория кода необходима быстрая загрузка тысяч узлов.

* **Neo4j/Memgraph/FalkorDB:** Используется конструкция UNWIND в Cypher, позволяющая передать список объектов в одном запросе и создать их пакетно.12  
* **Kùzu:** Предлагает команду COPY FROM, которая напрямую считывает CSV или Parquet файлы, минуя уровень интерпретации Cypher для каждого объекта, что в 18 раз быстрее традиционных методов.12  
* **Apache AGE:** Загрузка выполняется через SQL-запросы с использованием agtype, что позволяет использовать стандартные методы пакетной вставки Postgres.17

### **Инкрементальная синхронизация: Delete \+ Insert**

Особое требование HyperGraph — обновление связей при изменении файла. Паттерн «Delete+Insert» для исходящих ребер выглядит следующим образом:

1. Удаление всех существующих ребер типа LINKS\_TO от конкретного узла документа.  
2. Вставка нового набора ребер на основе текущего содержимого файла.

В Cypher это реализуется одной транзакцией:

Cypher

MATCH (d:Document {path: $path})  
OPTIONAL MATCH (d)--\>()  
DELETE r  
WITH d  
UNWIND $targets AS target\_path  
MERGE (t:Document {path: target\_path})  
MERGE (d)--\>(t)

Этот паттерн поддерживается всеми Cypher-совместимыми СУБД.50 Использование MERGE гарантирует идемпотентность создания целевых узлов (например, для еще не существующих файлов).50

## **Визуализация графов в веб\-интерфейсах**

Для фронтенда HyperGraph визуализация является не просто дополнением, а основным инструментом навигации. Исследование показывает, что лучше не привязываться к встроенным UI (таким как Neo4j Bloom или Memgraph Lab), а использовать специализированные JS-библиотеки.56

### **Сравнение JavaScript библиотек для визуализации**

| Библиотека | Технология | Производительность | Стиль | Интерактивность |
| :---- | :---- | :---- | :---- | :---- |
| **Cytoscape.js** | Canvas / DOM | Средняя (до 2k узлов) | CSS-подобный | Высокая |
| **Sigma.js** | WebGL | Очень высокая (50k+) | Программный | Средняя |
| **vis-network** | Canvas | Средняя | Конфигурационный | Высокая |
| **react-force-graph** | WebGL/Canvas | Высокая | Декларативный | Высокая |

**Sigma.js** рекомендуется для отображения глобального графа знаний проекта (десятки тысяч узлов), так как она использует WebGL для отрисовки, обеспечивая плавность при масштабировании.56 **Cytoscape.js** больше подходит для детальных представлений «окрестностей» конкретного документа (traversal), так как она обладает богатым набором алгоритмов автоматической раскладки и обработки событий.56

### **Готовые Open-Source UI**

Если требуется быстрое решение для отладки, можно рассмотреть:

* **Apache AGE Viewer:** Веб-интерфейс для AGE, позволяющий выполнять Cypher и видеть визуальное представление.18  
* **Neovis.js:** Библиотека, которая напрямую соединяется с базой через Bolt (Neo4j/Memgraph) и отрисовывает результат Cypher-запроса, используя мощь D3.js или vis.js.56  
* **Kùzu Explorer:** Инструмент для исследования графа Kùzu, поддерживающий панели запросов и схем.64

## **Реализация MVP: Индексация ссылок Obsidian**

Первым этапом MVP является индексация Markdown-ссылок. В этой задаче граф должен хранить относительные пути к файлам от корня проекта, что позволяет перемещать проект целиком без потери связей.

### **Базовые операции MVP**

1. **Поиск исходящих/входящих связей:**  
   MATCH (d:Document {path: 'doc1.md'})--\>(target) RETURN target.path  
2. **Обнаружение битых ссылок (Unresolved links):** MATCH (d:Document)--\>(t:Document) WHERE t.exists \= false RETURN d.path, t.label Здесь узлы для несуществующих файлов создаются с флагом exists: false при парсинге ссылок.53  
3. **Обход графа (Traversal):**  
   Поиск всех документов, связанных с текущим до глубины 3 шагов:  
   MATCH (d:Document {path: 'start.md'})--(neighbor) RETURN neighbor

## **Итоговые рекомендации и дорожная карта развития**

На основе проведенного анализа предлагается следующий план выбора и внедрения графовой СУБД для HyperGraph.

### **Рекомендация для MVP: Apache AGE или Kùzu**

Выбор между этими двумя решениями зависит от архитектуры Core-сервиса:

* **Вариант А (Apache AGE):** Если Core-сервис уже плотно завязан на PostgreSQL и требуется максимальная консистентность данных «реляционные таблицы \+ граф».2 Это решение обеспечивает лучшую изоляцию за счет использования отдельных БД в Postgres для каждого проекта.  
* **Вариант Б (Kùzu):** Если HyperGraph планируется как легкое приложение (например, десктопный инструмент), где запуск полноценного сервера Postgres избыточен.23 Kùzu обеспечивает высочайшую скорость аналитики и простоту развертывания.

### **Альтернатива для высоконагруженных RAG-систем: FalkorDB**

Если в будущем HyperGraph будет активно использовать ИИ-агентов для поиска по графу, FalkorDB станет лучшим выбором благодаря поддержке мультиграфовой изоляции в OSS-версии и встроенному векторному поиску.30

### **Дорожная карта (Roadmap)**

1. **Фаза 1 (MVP \- Markdown):**  
   * Развертывание выбранной СУБД (AGE или Kùzu) в Docker.  
   * Реализация парсера Markdown на Python, извлекающего \[\[links\]\].  
   * Настройка паттерна «Delete+Insert» для обновления связей.  
   * Интеграция Cytoscape.js для визуализации локального графа заметки.  
2. **Фаза 2 (Code Graph):**  
   * Добавление парсеров кода (Tree-sitter) для извлечения связей между функциями и классами.  
   * Использование Cypher для поиска зависимостей между кодом и документацией.  
3. **Фаза 3 (Multi-Project & Cross-Queries):**  
   * Реализация механизма switch(project\_id) для быстрого переключения контекста БД.  
   * (Для AGE) Исследование возможности межбазовых запросов через dblink или postgres\_fdw для анализа связей между вложенными проектами.  
4. **Фаза 4 (Optimization):**  
   * Переход на векторизованную загрузку данных.  
   * Внедрение Sigma.js для визуализации глобальных графов (10k+ узлов).

Внедрение графовой СУБД по модели «Project-first» позволит HyperGraph стать мощным аналитическим инструментом, сохраняя при этом гибкость и простоту управления данными, характерную для Git-ориентированных рабочих процессов.

#### **Источники**

1. Top 9 Open Source Graph Databases \- Analytics Vidhya, дата последнего обращения: марта 8, 2026, [https://www.analyticsvidhya.com/blog/2024/01/top-9-open-source-graph-databases/](https://www.analyticsvidhya.com/blog/2024/01/top-9-open-source-graph-databases/)  
2. Apache AGE Graph Database | Apache AGE, дата последнего обращения: марта 8, 2026, [https://age.apache.org/faq/](https://age.apache.org/faq/)  
3. Neo4j vs ArangoDB vs RedisGraph: Best Open-Source Graph, дата последнего обращения: марта 8, 2026, [https://blog.octabyte.io/topics/open-source-databases/neo4j-vs-arangodb-vs-redisgraph/](https://blog.octabyte.io/topics/open-source-databases/neo4j-vs-arangodb-vs-redisgraph/)  
4. Top 10 Graph Database Tools in 2025: Features, Pros, Cons, дата последнего обращения: марта 8, 2026, [http://www.bestdevops.com/top-10-graph-database-tools-in-2025-features-pros-cons-comparison/](http://www.bestdevops.com/top-10-graph-database-tools-in-2025-features-pros-cons-comparison/)  
5. 10 Best Open-Source NoSQL Databases for 2025 \- Neo4j, дата последнего обращения: марта 8, 2026, [https://neo4j.com/news/10-best-open-source-nosql-databases-for-2025/](https://neo4j.com/news/10-best-open-source-nosql-databases-for-2025/)  
6. Multiple databases \- Upgrade and Migration Guide \- Neo4j, дата последнего обращения: марта 8, 2026, [https://neo4j.com/docs/upgrade-migration-guide/current/version-4/migration/drivers/multiple-db/](https://neo4j.com/docs/upgrade-migration-guide/current/version-4/migration/drivers/multiple-db/)  
7. Neo4j Community Edition limitations, дата последнего обращения: марта 8, 2026, [https://community.neo4j.com/t/neo4j-community-edition-limitations/56106](https://community.neo4j.com/t/neo4j-community-edition-limitations/56106)  
8. Multiple database in community edition · Issue \#12920 \- GitHub, дата последнего обращения: марта 8, 2026, [https://github.com/neo4j/neo4j/issues/12920](https://github.com/neo4j/neo4j/issues/12920)  
9. Neo4J community edition DB size limit?, дата последнего обращения: марта 8, 2026, [https://dba.stackexchange.com/questions/186968/neo4j-community-edition-db-size-limit](https://dba.stackexchange.com/questions/186968/neo4j-community-edition-db-size-limit)  
10. what is the limitation in neo4j community edition in terms of data, дата последнего обращения: марта 8, 2026, [https://stackoverflow.com/questions/39659841/what-is-the-limitation-in-neo4j-community-edition-in-terms-of-data-storagei-e](https://stackoverflow.com/questions/39659841/what-is-the-limitation-in-neo4j-community-edition-in-terms-of-data-storagei-e)  
11. Open-source graph database, tuned for dynamic analytics ... \- GitHub, дата последнего обращения: марта 8, 2026, [https://github.com/memgraph/memgraph](https://github.com/memgraph/memgraph)  
12. Kùzu, an extremely fast embedded graph database \- The Data Quarry, дата последнего обращения: марта 8, 2026, [https://thedataquarry.com/blog/embedded-db-2/](https://thedataquarry.com/blog/embedded-db-2/)  
13. Multi-Tenancy in Graph Databases and Why Should You Care?, дата последнего обращения: марта 8, 2026, [https://memgraph.com/blog/why-multi-tenancy-matters-in-graph-databases](https://memgraph.com/blog/why-multi-tenancy-matters-in-graph-databases)  
14. Multi-tenancy \- Memgraph, дата последнего обращения: марта 8, 2026, [https://memgraph.com/docs/memgraph-lab/features/multi-tenancy](https://memgraph.com/docs/memgraph-lab/features/multi-tenancy)  
15. Announcing: Memgraph as a Multi-Tenant Graph Database, дата последнего обращения: марта 8, 2026, [https://memgraph.com/blog/announcing-memgraph-as-multi-tenant-graph-database](https://memgraph.com/blog/announcing-memgraph-as-multi-tenant-graph-database)  
16. Multi-tenancy (Enterprise) \- Memgraph, дата последнего обращения: марта 8, 2026, [https://memgraph.com/docs/database-management/multi-tenancy](https://memgraph.com/docs/database-management/multi-tenancy)  
17. Apache Age \- Medium, дата последнего обращения: марта 8, 2026, [https://medium.com/@usman.khan9805/apache-age-af26f78b9158](https://medium.com/@usman.khan9805/apache-age-af26f78b9158)  
18. ApacheAGE 1.4.0: Apache AGE is a PostgreSQL Extension ... \- PGXN, дата последнего обращения: марта 8, 2026, [https://pgxn.org/dist/apacheage/1.4.0/](https://pgxn.org/dist/apacheage/1.4.0/)  
19. GitHub \- apache/age: Graph database optimized for fast analysis, дата последнего обращения: марта 8, 2026, [https://github.com/apache/age](https://github.com/apache/age)  
20. Documentation: 18: H.1. apache\_age — graph database functionality, дата последнего обращения: марта 8, 2026, [https://postgrespro.com/docs/enterprise/current/apache-age](https://postgrespro.com/docs/enterprise/current/apache-age)  
21. Add More Flexibility To Your PostgreSQL Queries With Apache AGE, дата последнего обращения: марта 8, 2026, [https://dev.to/markgomer/add-more-flexibility-to-your-postgresql-queries-with-apache-age-4n36](https://dev.to/markgomer/add-more-flexibility-to-your-postgresql-queries-with-apache-age-4n36)  
22. Apache AGE Graph Database | Apache AGE, дата последнего обращения: марта 8, 2026, [https://age.apache.org/](https://age.apache.org/)  
23. Kùzu: Graph Learning Applications Need a Modern ... \- OpenReview, дата последнего обращения: марта 8, 2026, [https://openreview.net/pdf?id=Eg3MthXzeT](https://openreview.net/pdf?id=Eg3MthXzeT)  
24. Kùzu A fast, scalable graph database for analytical workloads, дата последнего обращения: марта 8, 2026, [https://www.youtube.com/watch?v=gsMW-cRvqfQ](https://www.youtube.com/watch?v=gsMW-cRvqfQ)  
25. Leveraging Kùzu and Cypher for Advanced Data Analysis, дата последнего обращения: марта 8, 2026, [https://cu-dbmi.github.io/set-website/2024/05/24/Leveraging-K%C3%B9zu-and-Cypher-for-Advanced-Data-Analysis.html](https://cu-dbmi.github.io/set-website/2024/05/24/Leveraging-K%C3%B9zu-and-Cypher-for-Advanced-Data-Analysis.html)  
26. Embedded databases (1): The harmony of DuckDB, Kùzu and, дата последнего обращения: марта 8, 2026, [https://thedataquarry.com/blog/embedded-db-1/](https://thedataquarry.com/blog/embedded-db-1/)  
27. KŮZU^\* Graph Database Management System \- CIDR, дата последнего обращения: марта 8, 2026, [https://www.cidrdb.org/cidr2023/papers/p48-jin.pdf](https://www.cidrdb.org/cidr2023/papers/p48-jin.pdf)  
28. FalkorDB \- GitHub, дата последнего обращения: марта 8, 2026, [https://github.com/FalkorDB/FalkorDB](https://github.com/FalkorDB/FalkorDB)  
29. FalkorDB \- Open-source graph database major update (C/Rust), дата последнего обращения: марта 8, 2026, [https://www.reddit.com/r/Database/comments/1lfcm8p/falkordb\_opensource\_graph\_database\_major\_update/](https://www.reddit.com/r/Database/comments/1lfcm8p/falkordb_opensource_graph_database_major_update/)  
30. Why I Chose FalkorDB Knowledge Graph Over Neo4j for Building a, дата последнего обращения: марта 8, 2026, [https://blog.stackademic.com/why-i-chose-falkordb-knowledge-graph-over-neo4j-for-building-a-rag-application-69b949080e2c](https://blog.stackademic.com/why-i-chose-falkordb-knowledge-graph-over-neo4j-for-building-a-rag-application-69b949080e2c)  
31. Multigraph Topology: Linear Scale & Isolation \- FalkorDB, дата последнего обращения: марта 8, 2026, [https://www.falkordb.com/news-updates/multigraph-topology-isolation-linear-scale/](https://www.falkordb.com/news-updates/multigraph-topology-isolation-linear-scale/)  
32. FalkorDBLite (Python) | FalkorDB Docs, дата последнего обращения: марта 8, 2026, [https://docs.falkordb.com/operations/falkordblite/falkordblite-py.html](https://docs.falkordb.com/operations/falkordblite/falkordblite-py.html)  
33. Graph Memory for LLM Agents with mem0-falkordb, дата последнего обращения: марта 8, 2026, [https://www.falkordb.com/blog/graph-memory-llm-agents-mem0-falkordb/](https://www.falkordb.com/blog/graph-memory-llm-agents-mem0-falkordb/)  
34. FalkorDB graph store plugin for Mem0 \- GitHub, дата последнего обращения: марта 8, 2026, [https://github.com/FalkorDB/mem0-falkordb](https://github.com/FalkorDB/mem0-falkordb)  
35. Graphiti \+ FalkorDB: Integration for Multi-Agent Systems, дата последнего обращения: марта 8, 2026, [https://www.falkordb.com/blog/graphiti-falkordb-multi-agent-performance/](https://www.falkordb.com/blog/graphiti-falkordb-multi-agent-performance/)  
36. FalkorDB Graph Database with GraphRAG for AI/ML and GenAI, дата последнего обращения: марта 8, 2026, [https://www.falkordb.com/](https://www.falkordb.com/)  
37. FalkorDB Docs: Home, дата последнего обращения: марта 8, 2026, [https://docs.falkordb.com/](https://docs.falkordb.com/)  
38. Portable graph database to ship with application? \- Reddit, дата последнего обращения: марта 8, 2026, [https://www.reddit.com/r/Database/comments/1kztpi5/portable\_graph\_database\_to\_ship\_with\_application/](https://www.reddit.com/r/Database/comments/1kztpi5/portable_graph_database_to_ship_with_application/)  
39. Seamless Data Migration \- Apache AGE, дата последнего обращения: марта 8, 2026, [https://age.apache.org/blog/2024-04-25-seamless-data-migration-migrating-apache-age-data-between-different-versions-of-postgresql/](https://age.apache.org/blog/2024-04-25-seamless-data-migration-migrating-apache-age-data-between-different-versions-of-postgresql/)  
40. GitHub \- vesoft-inc/nebula: A distributed, fast open-source graph, дата последнего обращения: марта 8, 2026, [https://github.com/vesoft-inc/nebula](https://github.com/vesoft-inc/nebula)  
41. GitHub \- dgraph-io/dgraph: high-performance graph database for, дата последнего обращения: марта 8, 2026, [https://github.com/dgraph-io/dgraph](https://github.com/dgraph-io/dgraph)  
42. Quick Start \- Apache AGE, дата последнего обращения: марта 8, 2026, [https://age.apache.org/getstarted/quickstart/](https://age.apache.org/getstarted/quickstart/)  
43. Persistence on Docker \- FalkorDB Docs, дата последнего обращения: марта 8, 2026, [https://docs.falkordb.com/operations/persistence.html](https://docs.falkordb.com/operations/persistence.html)  
44. Get going with Neo4j and Jupyter Lab through Docker \- Medium, дата последнего обращения: марта 8, 2026, [https://medium.com/data-science/get-going-with-neo4j-and-jupyter-lab-through-docker-a1994e0e95c6](https://medium.com/data-science/get-going-with-neo4j-and-jupyter-lab-through-docker-a1994e0e95c6)  
45. Bug: Adding Large number of edges causes database to crash, дата последнего обращения: марта 8, 2026, [https://github.com/kuzudb/kuzu/issues/4953](https://github.com/kuzudb/kuzu/issues/4953)  
46. PostgreSQL Backup \- pg\_dump & pg\_dumpall, дата последнего обращения: марта 8, 2026, [https://neon.com/postgresql/postgresql-administration/postgresql-backup-database](https://neon.com/postgresql/postgresql-administration/postgresql-backup-database)  
47. Introduction to Postgres Backups | Crunchy Data Blog, дата последнего обращения: марта 8, 2026, [https://www.crunchydata.com/blog/introduction-to-postgres-backups](https://www.crunchydata.com/blog/introduction-to-postgres-backups)  
48. Feature: persist Kuzu database in the cloud · Issue \#5194 \- GitHub, дата последнего обращения: марта 8, 2026, [https://github.com/kuzudb/kuzu/issues/5194](https://github.com/kuzudb/kuzu/issues/5194)  
49. Create a graph database in Neo4j using Python \- Medium, дата последнего обращения: марта 8, 2026, [https://medium.com/data-science/create-a-graph-database-in-neo4j-using-python-4172d40f89c4](https://medium.com/data-science/create-a-graph-database-in-neo4j-using-python-4172d40f89c4)  
50. falkordb-py-orm/docs/MIGRATION\_GUIDE.md at main \- GitHub, дата последнего обращения: марта 8, 2026, [https://github.com/FalkorDB/falkordb-py-orm/blob/main/docs/MIGRATION\_GUIDE.md](https://github.com/FalkorDB/falkordb-py-orm/blob/main/docs/MIGRATION_GUIDE.md)  
51. FalkorDB/falkordb-bulk-loader: A Python utility for building ... \- GitHub, дата последнего обращения: марта 8, 2026, [https://github.com/FalkorDB/falkordb-bulk-loader](https://github.com/FalkorDB/falkordb-bulk-loader)  
52. Import data from CSV files \- Kuzu DB, дата последнего обращения: марта 8, 2026, [https://kuzudb.github.io/docs/import/csv/](https://kuzudb.github.io/docs/import/csv/)  
53. Neo4j if a node has no outgoing edges delete that ... \- Stack Overflow, дата последнего обращения: марта 8, 2026, [https://stackoverflow.com/questions/64013350/neo4j-if-a-node-has-no-outgoing-edges-delete-that-node-otherwise-return-its-next](https://stackoverflow.com/questions/64013350/neo4j-if-a-node-has-no-outgoing-edges-delete-that-node-otherwise-return-its-next)  
54. Run your own transactions \- Neo4j Python Driver Manual, дата последнего обращения: марта 8, 2026, [https://neo4j.com/docs/python-manual/current/transactions/](https://neo4j.com/docs/python-manual/current/transactions/)  
55. Using Delete+Insert for Incremental Models \- Paradime Help Docs, дата последнего обращения: марта 8, 2026, [https://docs.paradime.io/app-help/concepts/dbt-fundamentals/model-materializations/incremental-materialization/using-delete+insert-for-incremental-models](https://docs.paradime.io/app-help/concepts/dbt-fundamentals/model-materializations/incremental-materialization/using-delete+insert-for-incremental-models)  
56. 15 Best Graph Visualization Tools for Your Neo4j Graph Database, дата последнего обращения: марта 8, 2026, [https://neo4j.com/blog/graph-visualization/neo4j-graph-visualization-tools/](https://neo4j.com/blog/graph-visualization/neo4j-graph-visualization-tools/)  
57. graphgeeks-lab/awesome-graph-universe \- GitHub, дата последнего обращения: марта 8, 2026, [https://github.com/graphgeeks-lab/awesome-graph-universe](https://github.com/graphgeeks-lab/awesome-graph-universe)  
58. You Want a Fast, Easy-To-Use, and Popular Graph Visualization, дата последнего обращения: марта 8, 2026, [https://memgraph.com/blog/you-want-a-fast-easy-to-use-and-popular-graph-visualization-tool](https://memgraph.com/blog/you-want-a-fast-easy-to-use-and-popular-graph-visualization-tool)  
59. Top 10 JavaScript Libraries for Knowledge Graph Visualization, дата последнего обращения: марта 8, 2026, [https://www.getfocal.co/post/top-10-javascript-libraries-for-knowledge-graph-visualization](https://www.getfocal.co/post/top-10-javascript-libraries-for-knowledge-graph-visualization)  
60. Introduction to Cytoscape.js: Visualizing Graphs in the Browser, дата последнего обращения: марта 8, 2026, [https://gili842.medium.com/introduction-to-cytoscape-js-visualizing-graphs-in-the-browser-ce09ad6aa610](https://gili842.medium.com/introduction-to-cytoscape-js-visualizing-graphs-in-the-browser-ce09ad6aa610)  
61. apache/age-viewer: Graph database optimized for fast analysis and, дата последнего обращения: марта 8, 2026, [https://github.com/apache/age-viewer](https://github.com/apache/age-viewer)  
62. Neo4j Graph Visualization | Tom Sawyer Software, дата последнего обращения: марта 8, 2026, [https://blog.tomsawyer.com/neo4j-graph-visualization](https://blog.tomsawyer.com/neo4j-graph-visualization)  
63. neovis.js \- Neo4j Contrib Repositories, дата последнего обращения: марта 8, 2026, [https://neo4j-contrib.github.io/neovis.js/classes/NeoVis.html](https://neo4j-contrib.github.io/neovis.js/classes/NeoVis.html)  
64. Documentation \- Kuzu DB, дата последнего обращения: марта 8, 2026, [https://kuzudb.github.io/docs/](https://kuzudb.github.io/docs/)
