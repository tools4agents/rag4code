# <Workflow Pack Name>

## Назначение

Этот pack хранит reusable workflow и step-specific artifacts для `<workflow-purpose>`.

## Что входит в pack

- [`workflow.md`](./workflow.md) — canonical workflow graph document.
- [`terms.md`](./terms.md) — workflow-local terminology, если нужна.
- [`setup_instructions.md`](./setup_instructions.md) — integration/adoption guide.
- step packs с `STEP.md` и `SKILL.md`.

## Как выполнять workflow

1. Прочитать project-local policy/binding.
2. Открыть `workflow.md`.
3. Перейти в нужный `workflow-step`.

## Как использовать в своем проекте

1. Прочитать `setup_instructions.md`.
2. Разложить templates в свой проект.
3. Заполнить project-local files.

## Куда идти дальше

- process graph — в `workflow.md`
- step execution — в `STEP.md` / `SKILL.md`
- templates/examples — в `resources/`
