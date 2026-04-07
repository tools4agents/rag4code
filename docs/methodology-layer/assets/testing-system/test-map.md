# Test Map

> Status: Draft  
> Scope: concrete [`testing-system asset`](../../../terms/project/terms/testing-system-asset.md) под названием `test-map`  
> Role: Source of Truth для baseline test index, suite navigation и documentation-first traceability model

## Назначение

Этот документ фиксирует первый concrete [`testing-system asset`](../../../terms/project/terms/testing-system-asset.md): `test-map`.

Он задает baseline систему хранения и навигации для test documentation, которая связывает suites, test cases и test implementation через file-first Source of Truth.

## Что задает `test-map`

`Test-map` отвечает на вопросы:
- где живет test index;
- где живут suite pages;
- какая traceability chain считается целевой;
- как агент и человек находят documentation roots и implementation roots;
- как testing documentation связана с engineering SoT и кодом.

## Baseline layout

Для первой итерации `test-map` использует такой baseline layout:

```text
docs/testing/
  test-map.md
  suites/
```

## Роли элементов layout

- `docs/testing/test-map.md` - канонический индекс testing layer.
- `docs/testing/suites/` - storage location для suite pages.

Конкретные test code roots не фиксируются globally этим asset.

Вместо этого каждая suite page должна документировать собственные:
- implementation roots;
- documentation roots;
- search anchors.

## Что считается test index

Для `test-map` каноническим индексом testing layer считается `docs/testing/test-map.md`.

Этот файл должен давать краткую карту test suites:
- suite name;
- suite identifier;
- scope summary;
- links на suite page;
- links на primary implementation files или declared implementation roots.

Индекс нужен для navigation и coverage overview, а не для полного пересказа test cases.

## Целевая traceability chain

Целевой моделью для `test-map` считается цепочка:

`requirement -> suite -> test case -> test implementation`

Где:
- `requirement` задает upstream intent или behavior expectation;
- [`test-suite`](../../../terms/project/terms/test-suite.md) задает documentation-level grouping;
- [`test-case`](../../../terms/project/terms/test-case.md) задает атомарную verification unit;
- [`test-implementation`](../../../terms/project/terms/test-implementation.md) задает code-level исполнение проверки.

На переходном этапе допустим упрощенный baseline `requirement -> suite -> test script`, но он рассматривается как промежуточная модель, а не целевое состояние.

## Связь с suite pages

`Test-map` не хранит детальную структуру каждого suite.

Эта ответственность принадлежит supporting document [`test-suites.md`](test-suites.md).

Важный invariant:
- suite page является canonical documentation entry для suite;
- `test-map.md` остается обзорным индексом testing layer.

## Связь с traceability conventions

`Test-map` не задает подробно identifier grammar и code-level metadata placement.

Эта ответственность принадлежит supporting document [`test-case-traceability.md`](test-case-traceability.md).

## Связь с knowledge lifecycle

`Test-map` не задает lifecycle знания в проекте.

Он предполагает, что проект использует какой-то [`knowledge-lifecycle asset`](../../../terms/project/terms/knowledge-lifecycle-asset.md), например `document-driven-development`.

Следствие:
- test documentation layer относится к engineering documentation, а не к operational artifacts;
- execution notes и temporary test research не должны подменять `docs/testing/` как Source of Truth.

## Связь с terms management

`Test-map` не задает glossary system.

Если в проекте есть [`terms-management-system asset`](../../../terms/project/terms/terms-management-system-asset.md), testing docs должны использовать его terminology baseline, а не дублировать определения терминов.

## Связь с derived graph

Этот asset проектируется как file-first SoT для будущего graph-backed traceability.

Следствие:
- markdown остается каноническим источником идентификаторов и links;
- code annotations и docstrings являются supporting traceability anchors;
- graph database позже строится как derived representation по markdown и коду, а не заменяет их как source layer.

## Что этот документ не делает

Этот документ не описывает:
- полный execution reporting lifecycle;
- CI reporting format;
- detailed layout тестового кода внутри `tests/`;
- contract policy;
- process model разработки.

## Связь с другими документами

Этот документ нужно читать вместе с:
- [`asset-taxonomy-and-composition-model.md`](../../asset-taxonomy-and-composition-model.md);
- [`documentation-lifecycle-layers.md`](../knowledge-lifecycle/documentation-lifecycle-layers.md);
- [`test-suites.md`](test-suites.md);
- [`test-case-traceability.md`](test-case-traceability.md);
- [`overview.md`](../../overview.md).

## Canonical invariants

- `test-map` является concrete [`testing-system asset`](../../../terms/project/terms/testing-system-asset.md).
- `docs/testing/test-map.md` является каноническим test index для этой системы.
- `docs/testing/suites/` является baseline storage location для suite pages.
- target traceability chain для этой системы - `requirement -> suite -> test case -> test implementation`.
- markdown остается canonical Source of Truth для testing documentation and traceability metadata.
- code-level metadata служит supporting anchor, а не заменой suite documentation.
