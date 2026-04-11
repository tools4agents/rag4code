# Карта scopes терминов

> Status: Draft  
> Scope: root terminology entry point для документации HyperGraph  
> Role: карта всех available terminology scopes и links на их `terms-map.md`

## 1. Назначение

Этот документ является root entry point для терминологии HyperGraph.

Он нужен, чтобы:

- дать человеку и агенту первую точку входа в `docs/terms/`;
- показать, какие terminology scopes существуют в проекте;
- дать links на все scoped `terms-map.md`;
- поддерживать progressive disclosure от scope map к individual term pages.

## 2. Карта scopes

| Scope | Назначение | Entry point |
| --- | --- | --- |
| `common` | Переносимая карта общих терминов, не привязанных жестко к одному проекту. | [`terms-map.md`](./common/terms-map.md) |
| `project` | Project-specific терминология HyperGraph и слоя `Project Methodology Runtime`. | [`terms-map.md`](./project/terms-map.md) |

## 3. Правила для scopes

- Каждый scope должен иметь свой `terms-map.md`.
- Individual term pages живут внутри `docs/terms/<scope>/terms/`.
- Scope должен быть достаточно цельным, чтобы его можно было переносить между проектами как reusable terminology package.

## 4. Связанные документы

- `common` scope: [`terms-map.md`](./common/terms-map.md)
- `project` scope: [`terms-map.md`](./project/terms-map.md)
