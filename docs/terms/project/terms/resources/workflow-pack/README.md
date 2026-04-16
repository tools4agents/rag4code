# Resources: `workflow-pack`

## Назначение

Эта папка хранит reusable templates для canonical files `workflow-pack`.

Она нужна, чтобы рядом с термином `workflow-pack` держать не только определение сущности, но и минимальный scaffolding для ее materialization на filesystem.

## Что лежит в папке

- [`README.template.md`](./README.template.md) — navigation entrypoint template
- [`workflow.template.md`](./workflow.template.md) — canonical workflow graph document template
- [`terms.template.md`](./terms.template.md) — workflow-local terms template
- [`setup_instructions.template.md`](./setup_instructions.template.md) — adoption/install guide template
- [`STEP.template.md`](./STEP.template.md) — step semantics template
- [`SKILL.template.md`](./SKILL.template.md) — step skill template

## Границы

- Эти templates не являются самими терминами.
- Они являются support resources рядом с термином `workflow-pack`.
- Project-specific заполнение и runtime execution state должны materialize-иться уже в конкретном workflow-pack и его exchange layer.
