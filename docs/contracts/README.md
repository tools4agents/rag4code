# Contracts Layer

> Status: Draft  
> Scope: границы слоя `docs/contracts/` для HyperGraph  
> Role: краткий навигатор и policy для contract artifacts без архитектурных объяснений

## 1. Назначение слоя

`docs/contracts/` хранит формальные контракты и краткие contract notes для их использования.

Этот слой не должен пересказывать архитектуру системы. Его задача — быть точкой истины для формальных boundary artifacts и точкой навигации к связанным contract notes, тестам и реализации.

## 2. Что считается contract artifact

В `docs/contracts/` должны жить:
- OpenAPI contracts;
- JSON Schema contracts;
- AsyncAPI contracts, если они появятся;
- contract notes с правилами использования;
- links на contract tests и consumer or producer implementations.

## 3. Что является Source of Truth

Для формального API или message contract источником истины должен быть machine-readable contract:
- OpenAPI;
- JSON Schema;
- AsyncAPI.

Markdown в этом слое не должен вручную дублировать схему поле за полем.

## 4. Что допустимо в Markdown рядом с контрактом

Рядом с формальным контрактом допустимо хранить короткие contract notes, которые объясняют:
- смысл контракта;
- когда его вызывать или использовать;
- важные ограничения;
- edge cases;
- связь с другими контрактами;
- ссылки на тесты, реализацию и связанные workflow.

Markdown должен отвечать на вопрос как использовать контракт, а не как он полностью выглядит формально.

## 5. Что не должно жить в `docs/contracts/`

В `docs/contracts/` не должны жить:
- архитектурные rationale;
- повторное описание system design;
- полная терминологическая карта;
- discussion notes по trade-offs;
- повторение `overview` или layer principles.

Такие объяснения должны жить в:
- `docs/principles.md`;
- `docs/methodology-layer/overview.md`;
- `docs/methodology-layer/principles.md`;
- `docs/specification/`;
- `docs/adr/`.

## 6. Рекомендуемый layout

Для каждой contract area рекомендуется структура вида:

```text
contracts/
  <contract-area>/
    openapi.yaml
    notes.md
```

Дополнительно могут появляться:
- schema files;
- examples;
- links на contract test suites.

## 7. Связь с HyperGraph

Контрактный слой должен быть пригоден для traceability.

Поэтому для каждого важного контракта желательно иметь links на:
- реализацию;
- contract tests;
- producer and consumer components;
- связанные workflow или steps, если это важно для использования.

## 8. Как использовать этот слой

Рекомендуемый маршрут чтения:
1. открыть формальный contract file;
2. открыть `notes.md`, если нужен смысл использования;
3. перейти по ссылкам к тестам, реализации и связанным artifacts.

Этот слой является формальным boundary layer, а не архитектурным explanation layer.