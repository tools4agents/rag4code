# Plan: Выделение packaging conventions для семейств methodology artifacts

## Контекст
В ходе проектирования `Project Methodology Runtime` стало понятно, что почти все ключевые сущности будут существовать не как одиночные файлы, а как наборы связанных artifacts с собственными packaging conventions.

Это уже видно на примере:
- role packs для `agent-role` и adapter projections;
- contract packages для формального контракта, contract notes и контрактных тестов;
- workflow artifacts, где overview workflow связан с `workflow-step` документами;
- возможных будущих packs для skills, rules и других reusable assets.

Связанные документы:
- `docs/methodology-layer/artifact-model.md`
- `docs/methodology-layer/workflow-and-roles.md`
- `docs/methodology-layer/interfaces-and-storage.md`
- `docs/contracts/README.md`
- `docs/methodology-layer/overview.md`
- `docs/methodology-layer/principles.md`

## Цель
Зафиксировать отдельный архитектурный документ, который опишет общие packaging conventions для разных семейств methodology artifacts, чтобы дальше использовать единый подход вместо разрозненных локальных решений.

## Проблема
Сейчас packaging logic обсуждается фрагментарно:
- для `agent-role` уже обсуждается `pack-oriented layout`;
- для контрактов уже обсуждается contract package;
- для workflow уже фактически появляется связка overview + step docs;
- для других семейств артефактов conventions пока не определены явно.

Если это не вынести в отдельный документ, возникнет риск:
- разных несовместимых layout patterns;
- дублирования rationale в разных specs;
- потери общего принципа reusable packaging.

## Целевое состояние
После выполнения плана должен появиться отдельный канонический документ, который описывает:
- какие семейства artifacts существуют;
- какие из них логично упаковывать в packs;
- какие файлы являются semantic core, а какие projection, notes или support artifacts;
- как pack layout соотносится с `Catalog Source of Truth`, `Project Portable Intent`, `Service-local Runtime State` и `Runtime Materialization State`.

Этот будущий документ не должен дублировать уже зафиксированные boundaries:
- `artifact-model.md` владеет artifact families и pack structure на уровне meta-model;
- `workflow-and-roles.md` владеет semantic usage роли и workflow assignment, но не canonical pack structure;
- `interfaces-and-storage.md` владеет storage boundary и location rules, но не contract policy;
- `docs/contracts/README.md` остается единственным Source of Truth для contract policy.

## Какие семейства артефактов нужно покрыть

### 1. `agent-role` packs
Нужно зафиксировать:
- core role artifact;
- adapter projections;
- docs внутри pack;
- связь core и projections.

Важно сохранить уже согласованный ownership:
- semantic role model принадлежит `docs/methodology-layer/workflow-and-roles.md`;
- pack structure и sibling artifact layout принадлежат artifact-oriented layer и будущему packaging doc.

### 2. Workflow packs
Нужно зафиксировать:
- workflow overview artifact;
- `workflow-step` artifacts;
- связь со `step-vacancy` и `agent-role`;
- возможные future bindings.

### 3. Contract packs
Нужно зафиксировать:
- formal contract file;
- contract notes;
- contract tests;
- links на producer and consumer implementations.

При этом нельзя нарушать уже зафиксированный invariant:
- contract policy и vocabulary не переносятся сюда как новый Source of Truth;
- packaging doc должен ссылаться на `docs/contracts/README.md`, а не дублировать его policy текст.

### 4. Skills and rules packs
Нужно обсудить:
- стоит ли skills и rules хранить как самостоятельные packs;
- где проходит граница между одиночным artifact и reusable pack.

### 5. Term packs или terminology bundles
Нужно обсудить:
- нужен ли packaging convention для reusable bundles терминов;
- как соотносятся `common` и `project` терминологические карты.

## Важные вопросы для обсуждения

- Что считать pack, а что просто directory layout?
- Когда family of artifacts заслуживает собственного pack-oriented convention?
- Где должны жить projections: внутри pack или в отдельном namespace?
- Как фиксировать связь core artifact и support artifacts?
- Как обеспечивать экспорт и переносимость packs между проектами?
- Как вписать contract tests и future runtime bindings в pack model?

## Предварительный архитектурный уклон
На текущем этапе уже зафиксированы следующие направляющие решения:
- reusable core semantics должны быть отделены от projections и support docs;
- pack — это packaging boundary, а не отмена semantic boundary;
- разные семейства артефактов могут иметь разные conventions, но внутри общего проекта нужен единый vocabulary и единый reasoning framework;
- packaging conventions продолжают artifact-oriented layer, а не process layer;
- role packs рассматриваются как artifact family, а не как способ смешать workflow semantics и pack layout;
- discussion и planning по packaging conventions остаются buffer layer в `tasks_descriptions/` до переноса результата в канонический doc.

## Следующий шаг
После утверждения этого плана нужно:
1. Использовать уже созданные канонические focused specs как boundary baseline.
2. Сравнить несколько семейств artifacts side by side.
3. Зафиксировать общие invariants упаковки и различия по семействам.
4. Сформировать canonical `docs/methodology-layer/packaging-conventions.md` без дублирования contract policy и process semantics.

## Ожидаемый результат
Packaging conventions перестают быть локальным знанием внутри отдельных discussion-docs и становятся управляемой частью общей архитектуры `Project Methodology Runtime`.