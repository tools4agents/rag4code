# Code Style

## Назначение

Этот файл фиксирует project-specific coding style и authoring conventions для HyperGraph.

Он дополняет technical baseline из `project/techContext.md`, но не подменяет architecture, contracts или methodology docs.

## Базовые правила

- Основной язык реализации - Python `3.13+`.
- Package and environment workflow строятся вокруг `uv`.
- Orchestration and environment control используют HSM там, где это релевантно.

## Язык в разных слоях

- Код, identifiers, docstrings, code comments и commit messages пиши на английском языке.
- Правила, skills и документацию проекта пиши на русском языке.
- Если для термина нет устойчивого русского аналога, используй общепринятый English term.

## Стиль Python-кода

- Предпочитай ясный, читаемый Python без лишней магии.
- Держи modules and functions компактными и с одной основной ответственностью.
- Избегай скрытых side effects и неявных глобальных зависимостей.
- Имена `modules`, `functions`, `variables` и field-like identifiers оформляй в `snake_case`.
- Имена `classes` оформляй в `PascalCase`.
- Public API, models и integration boundaries должны иметь предсказуемые имена и не дрейфовать между слоями.

## Стиль проектирования

- Отделяй reusable semantics от runtime-specific projection.
- Не смешивай architecture rationale, contract details и operational notes в одном артефакте.
- Предпочитай explicit contracts и explainable boundaries неявным соглашениям.
- File-first Source of Truth важнее derived runtime outputs.

## Работа с документацией и кодом

- Если изменение затрагивает public behavior, contracts или long-lived architecture, сначала обновляй relevant `docs/` artifacts.
- Temporary research, discussion и execution notes должны жить в `operational_scope/`, а не в `docs/`.
- Не дублируй glossary definitions в code-adjacent docs; используй канонические terms из `docs/terms/`.

## Тесты и качество

- Новое поведение должно сопровождаться релевантной проверкой на уровне component, contract или integration scope.
- Если меняется contract или observable behavior, синхронизируй tests и documentation вместе с кодом.
- Regression fixes должны сопровождаться проверкой сценария, который раньше ломался.

## Что этот файл не делает

Этот файл не задает:
- полную architecture policy;
- contract authoring policy;
- task-management process;
- Kilo-specific runtime rules.

Эти темы принадлежат другим слоям:
- `docs/` для engineering SoT;
- `operational_scope/` для execution artifacts;
- `.kilo/` для Kilo-specific rules and runtime behavior.

## Связанные файлы

- `project/techContext.md`
- `docs/principles.md`
- `docs/methodology-layer/principles.md`
- `docs/methodology-layer/naming-conventions.md`
- `docs/contracts/README.md`
