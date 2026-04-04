# Project Discovery for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая спецификация discovery policy для `Project Methodology Runtime`  
> Role: Source of Truth для `manual-hybrid discovery`, classification model и минимального project graph contract

## 1. Назначение документа

Этот документ фиксирует, как слой `Project Methodology Runtime` должен искать, классифицировать и связывать проекты.

Его задача — описать:
- как сервис находит project candidates;
- как heuristic signals сочетаются с developer-confirmed classification;
- как различаются root project, nested project, external reference и service-managed roots;
- как discovery влияет на indexing, graph isolation и cross-project navigation.

Этот документ не описывает:
- artifact meta-model;
- process semantics workflow and roles;
- storage state model вне discovery-specific implications;
- detailed MCP or Web UI contracts;
- contract policy.

## 2. Почему discovery является отдельным bounded context

`Project Discovery` нельзя считать простой файловой эвристикой по `.git`.

От него зависят:
- границы project scope;
- корректность graph isolation;
- различение nested projects и service-managed directories;
- качество cross-project navigation;
- безопасность indexing.

Если discovery сделать неявным или purely heuristic, система быстро станет непредсказуемой в monorepo-like layouts и в проектах со служебными directory trees.

## 3. Основной принцип

Базовый принцип discovery такой:
- filesystem heuristics ищут candidates;
- policy layer применяет classification model;
- final classification определяется не автоматически, а developer-confirmed decision;
- итоговая decision сохраняется как project-owned knowledge и используется дальше всеми зависимыми подсистемами.

Это и есть `manual-hybrid discovery`.

## 4. Discovery goals

`Project Discovery` должен решать пять задач:
- находить project root candidates;
- определять, какие из них считаются реальными projects для системы;
- определять отношения между проектами;
- исключать служебные и ignored roots;
- строить стабильную картину для indexing, navigation и graph projection.

## 5. Default heuristic

На первой итерации используется понятная default heuristic:
- directory с `.git` рассматривается как `project candidate`;
- directory с `.git` внутри уже найденного project root рассматривается как `nested project candidate`;
- наличие `.git` считается сильным сигналом, но не является окончательной истиной.

Следствие:
- heuristic запускает discussion и classification;
- final semantic meaning задает policy layer, а не raw filesystem scan.

## 6. Classification model

Каждый найденный candidate должен получить один из classification statuses.

### 6.1 `root-project`

Главный project root, относительно которого строится текущий project scope.

### 6.2 `nested-project`

Вложенный проект, который должен существовать как отдельный project node и индексироваться как отдельный scope.

### 6.3 `external-project-reference`

Внешний проект, важный для integration analysis, navigation или traceability.

Такой проект:
- может существовать локально или только как reference;
- не обязан индексироваться как editable local project;
- может использоваться как graph-visible external dependency or relation target.

### 6.4 `ignored-git-root`

Directory физически содержит `.git`, но для текущей системы не считается project root.

### 6.5 `service-managed-root`

Directory управляется самим сервисом и не должна рассматриваться как user project.

### 6.6 `unknown-candidate`

Candidate найден heuristic scan, но пока не получил подтвержденную classification decision.

## 7. Sources of truth for discovery decisions

Discovery decision не должна зависеть только от raw scan.

Нужно различать три источника:

### 7.1 Filesystem signals

Сигналы файловой системы:
- наличие `.git`;
- наличие service markers;
- наличие runtime markers;
- положение пути относительно project root;
- попадание в known ignored roots.

### 7.2 Project-level discovery knowledge

Проект должен хранить portable discovery decisions:
- какие nested projects подтверждены;
- какие git roots игнорируются;
- какие roots считаются service-managed;
- какие external project references известны проекту.

### 7.3 Service-level policy

Service settings должны задавать:
- default discovery roots;
- global ignore patterns;
- service-managed markers;
- technical roots, которые не должны трактоваться как user projects.

## 8. Discovery workflow

На первой итерации используется следующий lifecycle:
- scan filesystem for candidates;
- detect signals and markers;
- apply policy and existing known config;
- present ambiguous or new candidates for developer-confirmed classification;
- persist final decision;
- update project graph and downstream indexing scope.

## 9. Candidate scan

Candidate scan должен уметь работать в нескольких режимах:
- scan по known discovery roots;
- scan внутри уже зарегистрированного project root;
- scan по explicit path, если developer запускает targeted discovery.

Минимальный candidate record должен позволять хранить:
- `abs_path` или service-local reference;
- `rel_path_from_parent`, если есть parent project;
- `has_git`;
- `has_service_config`;
- `has_runtime_markers`;
- ignore or service markers, если они обнаружены.

## 10. Persistence of discovery result

Результат discovery должен сохраняться в двух формах:
- как project-owned confirmed decision;
- как service-local snapshot для diagnostics and audit.

Важный invariant первой итерации:
- автоматического повторного discovery не происходит;
- новый discovery выполняется только по явному запросу разработчика;
- classification не должна silently drift без участия человека.

## 11. Nested `.git` policy

Для nested `.git` фиксируется следующая policy:
- по умолчанию nested `.git` дает `nested project candidate`;
- но final meaning определяется человеком;
- nested `.git` не запрещен, но никогда не должен silently считаться окончательно валидным project scope без classification.

Это особенно важно для:
- nested repositories;
- vendor-like imported repos;
- service-generated roots;
- staging or cache directories.

## 12. Service-managed directories

Нужно явно различать user project roots и directories, создаваемые самим сервисом.

`Service-managed-root`:
- не является user project;
- не должен попадать в project graph как отдельный business project;
- не должен случайно индексироваться как nested project;
- должен иметь ignore semantics и для discovery, и для indexing.

Именно эта категория предотвращает загрязнение graph техническими directory trees.

## 13. External project references

Слой discovery должен уметь работать не только с local nested projects, но и с external references.

`External-project-reference` нужен, когда:
- другой проект важен для integration reasoning;
- нужно строить cross-project navigation;
- требуется traceability к consumer or provider project;
- локальное полное индексирование не является обязательным.

Такой reference должен храниться как stable project identity, а не как обязательный absolute path.

## 14. Minimal graph contract

Для первой итерации графовый contract discovery должен оставаться минимальным.

### 14.1 Vertex model

Достаточно одного vertex family:
- `Project`

У project node должны быть как минимум признаки:
- `project_id`
- `display_name`
- `project_kind` с различием local or external semantics
- `has_local_db`

### 14.2 Edge model

Достаточно двух edge families:
- `PARENT_OF`
- `USES_PROJECT`

Этого достаточно, чтобы:
- показывать nested relation;
- показывать external project usage;
- обеспечивать navigation по project boundaries.

Snapshots, ignored roots и service-managed decisions не обязаны материализоваться как отдельные graph nodes первой итерации.

## 15. Discovery and indexing

Discovery должен предшествовать indexing.

Именно discovery определяет:
- какие roots индексируются как текущий project scope;
- какие roots индексируются отдельно;
- какие paths исключаются;
- какие graph links должны вести на `Project`, а не на internal component node.

Если это разделение не зафиксировано, индексатор начнет:
- захватывать nested project как часть current project;
- включать service-managed directories в graph;
- ломать cross-project isolation.

## 16. Discovery and navigation

Корректная discovery policy нужна не только для indexing, но и для explainable navigation.

Человек или агент должны уметь понять:
- почему directory считается project;
- почему nested root игнорируется или выделяется отдельно;
- как project связан с другим project через graph;
- какой scope считается current root и какие scopes считаются external.

Именно поэтому discovery decision должна быть explainable, а не скрытой эвристикой.

## 17. Что этот документ не должен делать

Этот документ не должен:
- описывать storage state model во всем объеме;
- описывать interfaces beyond discovery-related implications;
- дублировать artifact model;
- дублировать workflow semantics;
- дублировать contract policy.

Если сюда начинают попадать runtime path rules, role semantics или contract authoring guidance, это означает нарушение boundaries.

## 18. Связь с другими каноническими документами

Этот документ нужно читать вместе с:
- `docs/methodology-layer/overview.md` как обзором слоя;
- `docs/methodology-layer/principles.md` как набором guiding principles;
- `docs/methodology-layer/interfaces-and-storage.md` как storage boundary spec;
- `docs/contracts/README.md` только если нужна связь discovery с traceability contracts;
- idea-level context documents про project-first architecture.

## 19. Canonical invariants

Для первой итерации migration baseline считаются обязательными следующие invariants:
- discovery работает как `manual-hybrid discovery`;
- наличие `.git` дает strong candidate signal, но не final classification;
- final classification подтверждается человеком;
- nested `.git` по умолчанию считается candidate, но не гарантирует отдельный project;
- `service-managed-root` должен быть исключен из user project semantics;
- `external-project-reference` допускается как first-class project relation;
- graph contract первого MVP остается минимальным: `Project` nodes плюс `PARENT_OF` и `USES_PROJECT`.

## 20. Целевое назначение для миграции legacy docs

При миграции legacy planning package этот документ должен стать канонической точкой сборки для:
- discovery heuristic baseline;
- classification statuses;
- developer-confirmed discovery workflow;
- nested git policy;
- service-managed root policy;
- minimal project graph contract.

После завершения миграции именно этот файл должен заменить временные planning explanations про project discovery, которые сейчас живут в legacy planning docs.