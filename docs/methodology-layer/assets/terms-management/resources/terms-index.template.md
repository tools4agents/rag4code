# Карта scopes терминов

> Status: Draft  
> Scope: root terminology entry point для <project-or-scope>  
> Role: карта всех available terminology scopes и links на их `terms-map.md`

## 1. Назначение

Этот документ является root entry point для терминологии `<project-or-scope>`.

Он нужен, чтобы:

- дать человеку и агенту первую точку входа в `docs/terms/`;
- показать, какие terminology scopes существуют в проекте;
- дать links на все scoped `terms-map.md`;
- поддерживать progressive disclosure от scope map к individual term pages.

## 2. Как пользоваться этим файлом

Рекомендуемый маршрут чтения:

1. найти нужный terminology scope;
2. перейти в его `terms-map.md`;
3. при необходимости открыть individual term page внутри `terms/`.

## 3. Карта scopes

| Scope | Назначение | Entry point |
| --- | --- | --- |
| `<scope-1>` | <What this terminology scope covers> | [`terms-map.md`](./<scope-1>/terms-map.md) |
| `<scope-2>` | <What this terminology scope covers> | [`terms-map.md`](./<scope-2>/terms-map.md) |

## 4. Правила для scopes

- Каждый scope должен иметь свой `terms-map.md`.
- Individual term pages живут внутри `docs/terms/<scope>/terms/`.
- Scope должен быть достаточно цельным, чтобы его можно было переносить между проектами как reusable terminology package.
- Если терминология scope становится слишком широкой или внутренне неоднородной, scope нужно разделять.

## 5. Политика обновления

Обновляй этот файл, если:

- добавился новый terminology scope;
- scope был удалён или переименован;
- изменился entry point scoped `terms-map.md`.

Этот файл — root terminology entry point для человека и агента.
