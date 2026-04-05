# agent-system materialization

> Status: Draft  
> Scope: project-specific term for HyperGraph runtime process model  
> Related: `docs/terms/terms_map.md`

## 1. Назначение термина

`Agent-system materialization` — это процесс, при котором HyperGraph раскладывает assets для выбранной `primary-agent-system` в конкретном проекте как runtime-facing artifacts.

## 2. Зачем нужен этот термин

Термин нужен, чтобы отделить:

- reusable source assets;
- `agent-system`-specific source assets;
- конечный runtime output, который реально потребляет environment.

Без этого distinction легко спутать source-layer authoring и runtime output generation.

## 3. Что делает materialization

`Agent-system materialization` включает:

- выбор релевантных `agent-system`-specific assets;
- разрешение project-specific selection вроде `primary-agent-system`;
- подготовку environment-facing runtime artifacts;
- раскладку этих artifacts в project-scoped runtime.

## 4. Что materialization не означает

`Agent-system materialization` не означает:

- что runtime output становится Source of Truth;
- что abstract assets теряют значение;
- что проект теперь навсегда привязан к одной `agent-system`.

Materialization является runtime process, а не semantic owner layer.

## 5. Связь с multi-developer model

Для одного и того же проекта разные разработчики могут использовать разные `agent-system`.

Поэтому materialization:

- зависит от выбранной в текущем developer context `primary-agent-system`;
- не обязана быть одинаковой для всех разработчиков;
- по возможности не должна засорять основной project repo runtime-specific artifacts.

## 6. Связанные термины

`Agent-system materialization` нужно читать вместе с:

- `agent-system`;
- `primary-agent-system`;
- `agent-system-agnostic asset`;
- `agent-system-specific asset`;
- `Runtime Materialization State`.
