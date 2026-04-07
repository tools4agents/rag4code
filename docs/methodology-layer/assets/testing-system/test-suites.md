# Test Suites

> Status: Draft  
> Scope: supporting specification для concrete [`testing-system asset`](../../../terms/project/terms/testing-system-asset.md) `test-map`  
> Role: Source of Truth для suite page structure, navigation metadata и search-boundary conventions

## Назначение

Этот документ задает baseline structure suite pages для `test-map`.

Его задача - описать:
- какую роль играет suite page;
- какие sections рекомендуется иметь;
- где фиксируются documentation roots и implementation roots;
- как агенту сузить search scope до нужной области.

## Роль suite page

Suite page - это canonical documentation entry для одного [`test-suite`](../../../terms/project/terms/test-suite.md).

Она нужна, чтобы:
- кратко описать scope suite;
- зафиксировать suite identifier;
- связать suite с requirement-level intent;
- указать, где искать implementation;
- указать, какие search anchors использовать человеку и агенту.

## Recommended suite page sections

Для первой итерации suite page рекомендуется делать со следующими sections:

1. `Suite ID`
2. `Purpose` или `Scope`
3. `Related requirements` или `Related artifacts`
4. `Documentation roots`
5. `Implementation roots`
6. `Search anchors`
7. `Test cases`
8. optional `Runbook`
9. optional `Notes`

## Documentation roots

`Documentation roots` должны указывать, где искать каноническую тестовую документацию для этого suite.

Обычно это:
- текущая suite page;
- `docs/testing/test-map.md`;
- другие related engineering docs, если suite зависит от contracts, ADR или architectural docs.

## Implementation roots

`Implementation roots` должны указывать directories или files, где обычно находится [`test-implementation`](../../../terms/project/terms/test-implementation.md) для этого suite.

Это нужно, чтобы:
- человек быстрее находил код;
- агент мог grep или читать только релевантную область;
- search scope не размазывался по всему repository.

Важно:
- testing-system asset не требует одного глобального layout тестового кода;
- suite page обязана зафиксировать local implementation roots для своей области.

## Search anchors

Каждая suite page должна задавать `search anchors`, пригодные для grep, regex и agent navigation.

Baseline anchors:
- `Suite: TS-...`
- `Test case: TC-<AREA>-<SUITE>-`
- `Requirement: REQ-...`

При необходимости можно добавлять:
- stable module names;
- package roots;
- contract identifiers.

## Test cases section

Section `Test cases` должен фиксировать краткую карту test cases suite.

Минимально рекомендуется хранить:
- `Test case ID`;
- краткое описание;
- related requirement identifiers;
- links или pointers на implementation location.

Для первой итерации допустим и компактный table format, и list format.

## File-level suite metadata

Если один test module реализует один suite, file-level metadata рекомендуется хранить в Python module docstring.

Пример:

```python
"""Provider OpenAI chat adapter tests.

Suite: TS-PROVIDERS-OPENAI-CHAT
"""
```

Это помогает:
- быстро grep-ать suite id в коде;
- AST-safe извлекать module-level suite metadata;
- не смешивать suite-level metadata с произвольными comments.

## Что этот документ не делает

Этот документ не фиксирует:
- полную grammar identifiers;
- function-level metadata placement;
- CI reporting model.

Эти вопросы принадлежат [`test-case-traceability.md`](test-case-traceability.md).

## Связь с другими документами

Этот документ нужно читать вместе с:
- [`test-map.md`](test-map.md);
- [`test-case-traceability.md`](test-case-traceability.md);
- [`testing-system asset`](../../../terms/project/terms/testing-system-asset.md).

## Canonical invariants

- suite page является canonical documentation entry для одного [`test-suite`](../../../terms/project/terms/test-suite.md).
- suite page должна задавать `Suite ID`, `Documentation roots`, `Implementation roots` и `Search anchors`.
- suite page должна помогать агенту сузить search scope до нужной области, а не заставлять искать по всему repository.
- если один test module реализует один suite, module docstring является preferred place для `Suite: TS-...` metadata.
