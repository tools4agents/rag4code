# HyperGraph

## О проекте

HyperGraph — open source проект для построения единого knowledge graph поверх кода, документации, задач и methodology artifacts для совместной работы людей и AI-агентов.

Репозиторий содержит и product code, и methodology assets. Документацию и контракты нужно воспринимать как first-class engineering artifacts.

## Как читать контекст

Используй такой порядок чтения:

1. `project/index.md` для repository boundaries, technical context и project-level navigation.
2. `docs/index.md` для engineering documentation map и Source of Truth entry points.
3. `operational_scope/index.md` для временного execution context текущей итерации.
4. `.kilo/` для Kilo-specific rules, agents, commands и skills.

Если временный planning или task artifact конфликтует с `docs/`, следуй `docs/`.

## Правила Source of Truth

- `docs/` — engineering Source of Truth для архитектуры, контрактов и долгоживущих technical decisions.
- `project/` дает durable repository context, а не architectural canon.
- `operational_scope/` — временный execution layer для plans, tasks, research и discussion artifacts.
- Не воспринимай временные operational artifacts как долгоживущую архитектурную документацию.

## Структура репозитория

- `services/` содержит независимые сервисы и MCP-oriented components.
- `hsm/` содержит Hyper Stack Manager и является nested repository со своим local context.
- `docs/` содержит архитектуру, principles, ADRs, контракты и другую долгоживущую engineering documentation.
- `project/` содержит durable repository context для людей и агентов.
- `.kilo/` содержит Kilo-specific project configuration.

## Ключевые Entry points

- `project/index.md`
- `docs/index.md`
- `operational_scope/index.md`

## Рабочий язык

- Правила, skills и документацию проекта пиши на русском языке.
- Если в русском языке нет устойчивого аналога, используй общепринятый English term.
- В коде, code comments, docstrings, identifiers и commit messages используй английский язык.
