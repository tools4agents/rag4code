Ниже первичный список open questions / white spots для перехода к архитектурной проработке. Это не task list реализации, а карта неопределенностей.

## 1. Project registry и lifecycle

### Open questions

- Где хранится registry зарегистрированных `project`?
- Может ли HyperGraph работать без глобального registry, только с explicit root path?
- Как выбирается active project для CLI?
- Как MCP agent указывает project context?
- Что происходит, если project root перемещен или удален?
- Как обнаруживать, что project database больше не соответствует root?

### White spot

Пока есть `project` как доменная сущность, но не определен lifecycle:

```text
create/register -> index -> query -> reindex -> remove/unregister
```

---

## 2. Project config format

### Open questions

- Где лежит `project-config`?
  - внутри project root;
  - рядом с DB;
  - в global HyperGraph home;
  - комбинированно?
- Какой формат config: YAML, TOML, JSON?
- Является ли config файлом под Git?
- Должен ли config быть portable между машинами?
- Как задаются exclude rules?
- Нужен ли include allowlist?
- Какие hard-excludes кроме `.git` существуют?

### White spot

Не определена policy: `project-config` — часть project SoT или operational setting HyperGraph.

---

## 3. Project database placement

### Open questions

- Где физически хранится `project-database`?
  - внутри project root;
  - в `.hypergraph/`;
  - в user cache dir;
  - в service-managed storage?
- Должна ли DB попадать под Git? Скорее нет, но нужно явно.
- Как связать DB с project id/root?
- Как безопасно удалить DB?
- Можно ли иметь несколько DB snapshots для одного project?

### White spot

Есть принцип “DB derived and rebuildable”, но нет physical storage ownership model.

---

## 4. Project identity

### Open questions

- Что является stable `project_id`?
  - generated UUID;
  - hash root path;
  - name from config;
  - Git remote/repo identity;
  - user-provided id?
- Что происходит при clone project в другое место?
- Что происходит при rename root directory?
- Нужно ли project id хранить в config?

### White spot

Для future cross-project graph project id критичен, но сейчас identity model не определена.

---

## 5. Git interaction boundary

### Open questions

- Должен ли HyperGraph хотя бы читать current branch/commit hash для reports?
- Нужно ли сохранять “indexed at commit” metadata?
- Нужно ли предупреждать, если current commit отличается от indexed commit?
- Что делать с dirty working tree?
- Должен ли move operation проверять Git status перед изменениями?

### White spot

Мы зафиксировали: пользователь отвечает за reindex после checkout. Но не решили, насколько HyperGraph должен быть Git-aware для safety diagnostics.

---

## 6. Stale index detection

### Open questions

- Как понять, что DB stale?
  - file hash;
  - mtime;
  - indexed commit;
  - full rescan;
  - manifest?
- Должны ли query operations работать на stale DB?
- Должны ли mutating operations требовать fresh index?
- Что возвращать агенту, если state suspected stale?

### White spot

Без stale policy move/remove reports могут быть опасны: агент будет принимать решения по устаревшему graph state.

---

## 7. Markdown parser strategy

### Open questions

- Какой parser использовать?
  - `markdown-it-py`;
  - `mistune`;
  - unified/remark через JS;
  - custom lightweight parser?
- Нужен ли AST или достаточно token stream?
- Как получать source ranges для ссылок?
- Как сохранять formatting при rewrite?
- Как обрабатывать malformed Markdown?

### White spot

Parser choice напрямую влияет на safe rewrite. Пока есть только boundary: не Markdown LSP.

---

## 8. Link syntax matrix

### Open questions

Какие link types входят в MVP?

- inline links: `[text](path.md)`;
- reference links;
- shortcut reference links;
- autolinks;
- image links;
- anchors: `file.md#section`;
- extensionless links;
- absolute links from root;
- wiki links;
- links to directories;
- links to non-md assets;
- URL-encoded paths;
- paths with spaces.

### White spot

Без MVP link syntax matrix невозможно корректно определить parser, resolver и rewrite behavior.

---

## 9. Link resolution semantics

### Open questions

- Как canonicalize paths?
- Как обрабатывать `.` / `..`?
- Как защищаться от выхода за root?
- Как обрабатывать symlinks?
- Разрешены ли links через symlink наружу root?
- Как обрабатывать case sensitivity на разных файловых системах?
- Как resolver выбирает target для extensionless links?
- Что делать с duplicate candidate targets?

### White spot

Root safety и deterministic resolution еще не формализованы.

---

## 10. Rewrite semantics для move

### Open questions

- Какие links safely rewriteable?
- Сохраняем ли original link style?
- Сохраняем ли anchors?
- Сохраняем ли title в Markdown link: `[x](a.md "title")`?
- Как переписывать reference definitions?
- Как переписывать links с aliases/wiki syntax?
- Что делать, если source file изменился между dry-run и apply?
- Должен ли apply требовать operation token/plan id из dry-run?

### White spot

Move is core MVP value, но transactional safety model пока не определена.

---

## 11. Remove impact report contract

### Open questions

- Что exactly входит в remove impact report?
- Как сортировать affected files?
- Нужна ли severity/classification?
- Нужно ли показывать suggested next actions?
- Должен ли report включать snippets вокруг ссылок?
- В каком формате report возвращается CLI и MCP?

### White spot

Мы определили product смысл remove impact report, но не определили machine-readable structure.

---

## 12. MCP contracts

### Open questions

- Какой набор MCP tools в MVP?
- Какие input/output schemas?
- Как передается project context?
- Как возвращаются errors?
- Как обеспечить machine-readable + human-readable report вместе?
- Нужны ли dry-run/apply split tools или один tool с mode?
- Нужна ли защита от destructive operations через explicit confirmation?

### White spot

MCP — first-class interface, но контракты еще не определены.

---

## 13. CLI command model

### Open questions

- Как выглядит CLI namespace?
- Команды:
  - `project register`;
  - `project reindex`;
  - `links incoming`;
  - `links outgoing`;
  - `move plan`;
  - `move apply`;
  - `remove impact`?
- Как CLI выбирает project?
- Какие output modes нужны: human/table/json?
- Должен ли CLI быть thin wrapper over same use cases as MCP?

### White spot

CLI зафиксирован как first-class, но command model не определен.

---

## 14. Storage backend decision

### Open questions

- ArcadeDB точно нужен для MVP или overkill?
- Может ли MVP стартовать с SQLite?
- Нужна ли embedded DB или external service?
- Как хранить typed vertices/edges?
- Как выполнять traversal?
- Как обеспечить rebuild speed?
- Как тестировать storage adapter?
- Как мигрировать schema?

### White spot

Есть storage capability requirements, но нет ADR по backend.

---

## 15. Data model / schema

### Open questions

Какие минимальные entities?

- Project;
- FileNode;
- LinkRecord;
- GraphEdge;
- IndexRun;
- IndexState;
- OperationPlan;
- ImpactReport?

Какие поля обязательны?

- path;
- file hash;
- mtime;
- file type;
- semantic type;
- tags;
- link raw target;
- resolved target;
- source range;
- resolution status.

### White spot

Нужна conceptual data model до schema.

---

## 16. Transaction and safety model

### Open questions

- Как обеспечить atomic-ish move?
- Что делать при partial failure?
- Нужен ли backup?
- Нужен ли rollback?
- Сначала move file или rewrite incoming links?
- Как защищаться от concurrent file changes?
- Как проверять post-condition: no old incoming links remain?

### White spot

Safety — главный architecture driver, но механизм пока не определен.

---

## 17. File operations boundary

### Open questions

- Core сам пишет файлы или возвращает patches?
- CLI/MCP adapter применяет patches или core?
- Есть ли WorkspaceEdit-like abstraction?
- Как представлять planned file changes?
- Как сохранять line endings?
- Как сохранять encoding?

### White spot

Не решено: HyperGraph — planning engine, applying engine или оба.

---

## 18. Watcher vs explicit indexing

### Open questions

- В MVP только explicit reindex?
- Нужен ли file watcher позже?
- Если watcher есть, как он взаимодействует с Git checkout?
- Как debounce changes?
- Как обрабатывать massive branch switch?

### White spot

Мы склоняемся к explicit reindex, но архитектурно нужно не закрыть путь к watcher.

---

## 19. Semantic type assignment

### Open questions

- Как определить, что Markdown file — `term`?
  - path convention;
  - frontmatter;
  - config rule;
  - filename/location;
  - explicit registry?
- Как определить ADR, requirement, test case в future?
- Можно ли пользователю задавать custom semantic types?
- Как semantic type влияет на graph queries?

### White spot

`semantic_type` зафиксирован, но classification mechanism отсутствует.

---

## 20. Tags and properties

### Open questions

- Где задаются tags?
- Из frontmatter?
- Из config?
- Из derived heuristics?
- Как tags отличаются от semantic type?
- Какие tags нужны в MVP?
- Нужен ли tag filtering в первой реализации или только architecture readiness?

### White spot

Filtering by tags — product direction, но data source tags пока не определен.

---

## 21. Error model

### Open questions

- Какие error categories?
  - path outside root;
  - file not indexed;
  - stale index;
  - unsupported link;
  - unresolved link;
  - conflicting target path;
  - permission denied;
  - parser failure;
  - storage unavailable.
- Какие errors fatal для операции?
- Какие warnings допустимы?

### White spot

Без uniform error model CLI/MCP будут расходиться.

---

## 22. Report model

### Open questions

- Единый report object для CLI/MCP или разные?
- Что значит machine-readable + human-readable?
- Как report references source ranges?
- Нужно ли включать before/after link target?
- Нужен ли report id?
- Нужно ли сохранять reports в DB?

### White spot

Explainability зафиксирована как принцип, но report schema отсутствует.

---

## 23. Testing strategy

### Open questions

- Какие golden fixtures нужны для Markdown links?
- Как тестировать path resolution?
- Как тестировать rewrite?
- Как тестировать root escape protection?
- Как тестировать symlink behavior?
- Как тестировать DB rebuild idempotency?
- Как тестировать CLI/MCP consistency?

### White spot

Test design еще не начат, но для safe refactoring engine он критичен.

---

## 24. Performance assumptions

### Open questions

- Какой размер проекта считать target MVP?
  - 100 md files?
  - 1k?
  - 10k?
- Какая acceptable indexing latency?
- Какая acceptable query latency?
- Нужна ли incremental indexing в MVP?
- Нужны ли benchmarks на реальных hyper-projects?

### White spot

Нет performance envelope, поэтому трудно выбрать storage/parser.

---

## 25. Security and path safety

### Open questions

- Как обрабатывать symlinks?
- Как canonicalize absolute paths?
- Как защищаться от `../../outside-root`?
- Разрешены ли operations on hidden dirs besides `.git`?
- Как работать с permissions errors?
- Нужно ли sandbox-like policy?

### White spot

Root boundary зафиксирован, но конкретная safety policy нет.

---

## 26. Documentation vs code artifact boundary

### Open questions

- Когда и как вводить source code files?
- Будут ли `.py` files indexed as file nodes в early phase?
- Или code artifact graph строго future?
- Как не сломать Markdown MVP, расширяя на code?

### White spot

Future code artifact direction есть, но extension boundary нужно будет отдельно спроектировать.

---

## 27. Architecture decision backlog

Вероятные ADR/decision candidates:

- storage backend;
- parser strategy;
- project config location and format;
- project database location;
- project id strategy;
- link syntax MVP matrix;
- path resolution and symlink policy;
- dry-run/apply transaction model;
- CLI/MCP contract shape;
- stale index policy.

## Самые критичные вопросы для следующего архитектурного шага

Если двигаться методично, я бы первым блоком взял:

1. Project identity / registry / config / DB placement.
2. Link syntax matrix.
3. Path resolution and root safety.
4. Parser strategy.
5. Storage backend options.
6. Dry-run/apply safety model.
7. CLI/MCP operation contracts.

Именно эти решения определяют каркас первой реализации.