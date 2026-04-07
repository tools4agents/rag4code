# Test Case Traceability

> Status: Draft  
> Scope: supporting specification для concrete [`testing-system asset`](../../../terms/project/terms/testing-system-asset.md) `test-map`  
> Role: Source of Truth для identifier conventions, traceability chain и code-level metadata placement

## Назначение

Этот документ задает traceability conventions для testing documentation и test implementation.

Его задача - описать:
- целевую traceability chain;
- grammar identifiers;
- placement rules для suite, test case и requirement metadata;
- conventions, удобные для grep, regex, AST parsing и agent navigation.

## Целевая traceability chain

Для `test-map` целевой считается цепочка:

`requirement -> suite -> test case -> test implementation`

В этой цепочке:
- [`test-suite`](../../../terms/project/terms/test-suite.md) группирует связанный набор проверок;
- [`test-case`](../../../terms/project/terms/test-case.md) задает атомарную documented verification unit;
- [`test-implementation`](../../../terms/project/terms/test-implementation.md) задает исполнимый кодовый anchor.

## Identifier families

Для первой итерации фиксируются три baseline families:
- `REQ-<AREA>-<NNN>` для requirement identifiers;
- `TS-<AREA>-<SUITE>` для suite identifiers;
- `TC-<AREA>-<SUITE>-<NNN>` для test case identifiers.

Примеры:
- `REQ-PROVIDERS-012`
- `TS-PROVIDERS-OPENAI-CHAT`
- `TC-PROVIDERS-OPENAI-CHAT-003`

Главные требования к identifier:
- стабильность;
- уникальность в пределах проекта;
- отсутствие пробелов;
- grep-friendly and regex-friendly shape.

## Почему prefixes обязательны

Entity prefixes фиксируются явно:
- `REQ-`
- `TS-`
- `TC-`

Это нужно, чтобы:
- не путать suite ids, test cases и другие slugs;
- сделать поиск точнее;
- упростить автоматическую валидацию;
- облегчить будущую graph-backed traceability.

## Code-level metadata keys

Для code-level metadata фиксируются human-readable fixed keys:
- `Suite:`
- `Test case:`
- `Requirement:`

Примеры:

```text
Suite: TS-PROVIDERS-OPENAI-CHAT
Test case: TC-PROVIDERS-OPENAI-CHAT-003
Requirement: REQ-PROVIDERS-012
```

Именно эти fixed keys считаются baseline convention для grep, regex и agent navigation.

## Placement rules

### Module level

Если один test module реализует один suite, suite metadata рекомендуется ставить в module docstring.

Пример:

```python
"""Provider OpenAI chat adapter tests.

Suite: TS-PROVIDERS-OPENAI-CHAT
"""
```

### Class level

Class-level suite metadata допустима как optional grouping layer, если класс представляет осмысленную подгруппу tests внутри suite.

Но class-level metadata не должна заменять module-level или suite-page ownership.

### Function level

Function-level docstring является preferred place для `Test case:` и `Requirement:` metadata.

Пример:

```python
def test_returns_429_when_quota_exhausted():
    """Returns 429 when provider quota is exhausted.

    Test case: TC-PROVIDERS-OPENAI-CHAT-003
    Requirement: REQ-PROVIDERS-012
    """
```

## Relation to docstring style

Python docstrings могут использовать Google style как общий baseline для code documentation.

Testing traceability metadata не заменяет обычный docstring, а дополняет его structured lines для navigation and parsing.

То есть:
- обычный explanatory docstring сохраняется;
- `Suite:`, `Test case:` и `Requirement:` добавляются как фиксированные metadata lines.

## Search and grep policy

Conventions проектируются так, чтобы агент или человек мог сузить поиск до нужной области.

Практически это означает:
- если нужна suite documentation, search должен начинаться в `docs/testing/`;
- если нужна test implementation, search должен начинаться с `Implementation roots`, указанных в suite page;
- поиск по `TS-`, `TC-` и `REQ-` identifiers должен быть тривиальным через grep или regex.

## Recommended regex baseline

Для первой итерации достаточно такой baseline grammar:

```regex
^Suite:\s+(TS-[A-Z0-9-]+)$
^Test case:\s+(TC-[A-Z0-9-]+)$
^Requirement:\s+(REQ-[A-Z0-9-]+)$
```

## Что этот документ не делает

Этот документ не задает:
- CI execution reports;
- automated testcase generation policy;
- requirement authoring model;
- full project test layout.

## Связь с другими документами

Этот документ нужно читать вместе с:
- [`test-map.md`](test-map.md);
- [`test-suites.md`](test-suites.md);
- [`testing-system asset`](../../../terms/project/terms/testing-system-asset.md);
- [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md).

## Canonical invariants

- target traceability chain - `requirement -> suite -> test case -> test implementation`.
- `REQ-`, `TS-` и `TC-` являются baseline identifier families.
- `Suite:`, `Test case:` и `Requirement:` являются baseline code-level metadata keys.
- module docstring является preferred place для suite metadata, если один module реализует один suite.
- function docstring является preferred place для `Test case:` и `Requirement:` metadata.
- code-level metadata дополняет documentation SoT, а не заменяет его.
