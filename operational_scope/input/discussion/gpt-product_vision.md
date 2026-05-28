Идея у нас есть документация в проекте в виде макрдаун файлов кторые ссылаются друг на друга.
Например hyper-eval-kit/operational_scope/initiatives/product-vision
Допустим у нас есть термины в проекте hyper-graph/docs/methodology-layer/assets/terms-management
Они используются в разных местах. Или есть какой то макркдаун файл который мы решили переименовать и переместить в другое место.
Проблема: в маркдаун файле мы видим только ссылки исходящие из маркдаун файла в другие файлы, но мы не видим кто ссылается на наш маркдаун файл.
При переименовании и перемещении ИИ агенту нужно искать регулярными выражениями или grep все файлы которые ссылались на наш маркдаун файл. Менять ссылки определять отностеьные пути делать много рутинной работы.
Вспомним как работает Obsidian. Мы переименовали маркдаун заметку переместили ее в другое место и Obsidian автоматически пересчитал все ссылки в других файлах.
Мы хотим сделать подобный MCP инстурмент для ИИ агентов.
Мы указываем сервис папку проекта в нашей ОС он ее фиксирует.
Эта папка проекта считается корневой.
Дальше наш сервис проходит алгоритмом и обрабатывает все ссылки которые есть в маркдаун файлах.
Сервис имеет графовую БД. Каждая вершина графа в БД то маркдаун файл.
У нас есть все входящие и все исходящие ссылки дял каждого маркдаун файла.
Мы хотим дать ИИ агенту удобные инструменты:
- узнать список файлов на которы ссылается маркдаун файл
- узнать список файлов которые ссылаются на маркдаун файл
- move - переименовать/ переместить маркдаун файл в новое место с автоматическим обновлением всех ссылок во всех файлах которые на него ссылаются.
- remove - удалить мардаун документ и все упоинания о нем в файлах которые на него ссылались.
Т.е. переложить контроль на связзаность ссылко между маркдаун файлами на алгоритм, который работает быстро и уменьшить рутинную нагрузку на ИИ агента, освобождая его творческий ум для более интересных задач.

Да, похожие вещи уже существуют, но именно в комбинации:

* Markdown knowledge graph
* bidirectional links
* automatic refactoring of links on move/rename
* MCP server для ИИ агентов
* graph DB + semantic/document tooling

— это пока довольно новая и не до конца занятая ниша.

Твоя идея очень похожа на перенос модели работы Obsidian в мир agentic tooling и MCP.

Сейчас экосистема скорее разрозненная:

---

# Что уже существует

## 1. Obsidian-подобные системы

### Obsidian

Умеет:

* graph links
* backlinks
* automatic rename refactor
* wikilinks
* vault graph

Но:

* это desktop app
* не MCP
* не ориентировано на ИИ агентов
* нет API уровня "safe markdown refactoring engine"

---

### Logseq

Тоже имеет:

* backlinks
* graph structure
* markdown/org graph

Но опять:

* это knowledge app
* не infra/tooling layer для AI agents

---

# 2. LSP-подход (очень близко по духу)

То, что ты описываешь, концептуально ОЧЕНЬ похоже на:

## Language Server Protocol

Что делает LSP:

* references
* rename symbol
* go to definition
* find usages
* refactor safely

Ты фактически предлагаешь:

# Markdown Language Server + Graph Refactoring Engine + MCP

Это очень сильная идея.

---

# 3. Existing markdown link tools

Есть отдельные инструменты:

* markdown-link-check
* markdownlint
* remark
* unified ecosystem
* mkdocs plugins
* Docusaurus link validators

Но они обычно:

* валидируют ссылки
* иногда строят dependency graph
* НЕ делают transactional rename refactoring

---

# 4. Graph databases

Твой graph DB подход очень хороший.

Обычно используют:

* Neo4j
* ArangoDB
* SQLite graph tables
* embedded graph indexes

Но многие existing markdown tools вообще не доходят до graph DB.
Они просто делают filesystem scan + regex.

---

# Что сейчас появляется в AI ecosystem

Вот тут начинается самое интересное.

После появления:

* MCP
* agentic IDE
* Claude Code style agents
* repo-scale refactoring agents

возникла огромная проблема:

# AI agents плохо делают safe filesystem refactoring

Особенно:

* relative paths
* moved docs
* backlinks
* broken references
* wiki links
* transclusion
* embedded assets

То есть ты очень точно попал в реальную боль.

---

# По сути ты предлагаешь

Не просто markdown tool.

А:

# Documentation Refactoring Runtime

или

# Knowledge Graph Refactoring Engine

---

# Это уже почти:

* "Git for knowledge structure"
* "LSP for markdown graphs"
* "Symbol table for documentation"
* "AST/refactoring engine for docs"

---

# Почему grep/regex — плохой уровень abstraction

Ты очень правильно заметил проблему.

ИИ агент сейчас делает:

1. grep
2. regex replace
3. relative path recompute
4. heuristic validation

Это:

* дорого
* хрупко
* context-heavy
* token expensive
* unsafe

---

# А твой сервис делает

Агент говорит:

```json
move(
  from="docs/vision/product.md",
  to="docs/strategy/product-vision.md"
)
```

Сервис:

* знает graph
* знает backlinks
* знает all incoming refs
* пересчитывает relative paths
* atomically updates refs
* validates consistency

ИИ агент освобождается от:

* path math
* grep
* regex
* filesystem traversal

Это очень сильное architectural separation.

---

# Это особенно хорошо для agentic systems

Потому что ИИ агент:

* плохо работает с global consistency
* плохо делает deterministic refactoring
* плохо держит state больших knowledge graphs

А алгоритмический engine:

* отлично делает это

---

# По сути это:

## "Infrastructure binding for documentation graph"

Очень похоже на ваши прошлые обсуждения:

* orchestration
* artifact-driven systems
* infrastructure abstraction

Только теперь artifact = markdown node.

---

# Как я бы это концептуально назвал

Варианты:

* Markdown Graph Runtime
* Knowledge Graph Refactoring Engine
* Documentation Graph Infrastructure
* Markdown Link Orchestrator
* DocGraph MCP
* Knowledge Graph MCP
* Semantic Markdown Runtime

---

# Какие MCP инструменты могли бы быть

Например:

```ts
get_outgoing_links(path)
get_incoming_links(path)

move_document(old_path, new_path)

remove_document(path)

rename_document(path, new_name)

get_broken_links()

reindex_workspace()

find_orphan_documents()

get_graph_neighbors(path)

search_by_tag(tag)

search_semantic(query)
```

---

# Очень важная идея

Ты интуитивно пришел к:

# Documentation as structured graph

а не:

# Documentation as plain text files

Это огромная разница.

---

# Еще глубже: это уже похоже на compiler architecture

Почти буквально:

| Compiler        | Твой сервис        |
| --------------- | ------------------ |
| Source file     | Markdown file      |
| Import graph    | Link graph         |
| Symbol table    | Document registry  |
| Rename symbol   | Rename document    |
| Find references | Incoming links     |
| AST             | Parsed markdown    |
| Linker          | Reference resolver |

Это очень хорошая архитектурная аналогия.

---

# Чего сейчас особенно не хватает на рынке

Именно:

## AI-native documentation infrastructure

Сейчас почти все инструменты:

* human-first
* IDE-first
* note-taking-first

А у тебя:

* agent-first
* refactoring-first
* graph-native
* consistency-oriented

Это уже новое поколение tooling.

---

# Я бы еще добавил

## 1. Transactional operations

```ts
begin_transaction()
move()
rename()
remove()
commit()
rollback()
```

---

## 2. Reference types

Разделять:

* hard links
* semantic refs
* wiki refs
* embeds
* transclusions
* tags
* aliases

---

## 3. AST parsing вместо regex

Очень важно.

Не regex replace.

А:

Markdown AST:

* mdast
* remark AST

И refactoring поверх AST.

---

# Особенно мощная идея

Если сделать:

# filesystem + graph db + MCP + AST

То получится почти:

# "LSP for knowledge systems"

И это уже очень серьезный infrastructure layer для AI-native SDLC.
