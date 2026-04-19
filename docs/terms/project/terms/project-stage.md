# project-stage

> Status: Draft  
> Scope: project-specific term for staged execution and delivery planning  
> Related: `../terms-map.md`

`Project stage` — это крупная bounded phase внутри execution plan проекта, которая группирует связанные задачи и задает dependency order между ними.

`Project stage` нужен, чтобы:

- разделять крупные слои работы вроде documentation SoT, structure materialization и implementation;
- не смешивать upstream design decisions и downstream execution в одном проходе;
- делать handoff и continuation между агентами и сессиями более явными;
- упрощать staged `task-map` и small-batch execution.

Основная operational materialization surface для `project stage` обычно фиксируется через [`task-map`](../../../methodology-layer/assets/task-management/task-map.md).

`Project stage` не равен отдельному [`task artifact`](./task-artifact.md).

Он задает более крупный уровень decomposition, внутри которого уже появляются конкретные task entries и при необходимости отдельные task files.

В рамках staged execution обычно ожидается, что следующий `project stage` не открывается полностью, пока предыдущий stage не достиг достаточного уровня stabilization.
