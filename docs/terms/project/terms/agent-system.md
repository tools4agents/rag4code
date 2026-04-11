# agent-system

> Status: Draft  
> Scope: project-specific term for HyperGraph methodology and runtime model  
> Related: `docs/terms/index.md`

## 1. Назначение термина

`agent-system` — это ПО для работы с coding agents на базе LLM, у которого есть собственная модель `agent-role`, rules, tools и runtime artifacts.

HyperGraph не сводит все такие системы к одной runtime model, а рассматривает их как разные target environments, для которых могут потребоваться разные compatible assets и разные правила materialization.

## 2. Зачем нужен этот термин

Термин нужен, чтобы отделить:

- reusable abstract assets HyperGraph;
- `agent-system`-specific assets;
- runtime materialization внутри конкретного проекта.

Без этого различия архитектура быстро начинает путать:

- core domain model;
- adapter- or system-specific representations;
- конечные runtime artifacts, которые реально потребляет environment.

## 3. Что описывает `agent-system`

На уровне HyperGraph `agent-system` задает внешний runtime target, у которого есть собственные:

- `agent-role` or agent profile model;
- rules and instructions model;
- tools or tool-access model;
- runtime artifacts и expected filesystem layout;
- ограничения и capabilities, которые влияют на materialization.

Примеры возможных `agent-system`:

- Kilo;
- Cursor;
- другие будущие coding-agent environments.

## 4. Связь с reusable assets

HyperGraph различает:

- `agent-system`-agnostic assets;
- `agent-system`-specific assets.

Например:

- methodology asset часто является `agent-system`-agnostic;
- abstract `agent-role` asset тоже может быть `agent-system`-agnostic;
- файл вроде `agent_roles/critic/agent_systems/kilo/role.md` является `agent-system`-specific asset.

## 5. Связь с проектом и разработчиком

Проект сам по себе не должен зависеть от одной конкретной coding agent system.

В нормальной модели:

- проект сохраняет reusable и portable assets;
- разные разработчики могут использовать разные `agent-system` для работы с одним и тем же проектом;
- настройки конкретной `agent-system` должны по возможности жить изолированно и не загрязнять основной project repo.

Типичный сценарий:

- разработчик 1 работает через Kilo;
- разработчик 2 работает через Cursor;
- каждый из них держит system-specific настройки в своем изолированном слое, например в nested git repo.

Такой подход позволяет:

- не прибивать проект к одной agent system;
- не превращать основной проект в смесь runtime settings разных environments;
- сохранять свободу выбора инструмента для каждого разработчика.

## 6. Связь с materialization

`Agent-system` не равен runtime artifact.

Он является target environment, под который HyperGraph:

- выбирает совместимые `agent-system`-specific assets;
- разрешает adapter-specific distinctions;
- materialize environment-facing runtime artifacts в проекте.

Именно поэтому нужно различать:

- `agent-system` как target system;
- `agent-system`-specific asset как source artifact под эту систему;
- `agent-system materialization` как runtime process.

## 7. Что не стоит смешивать с `agent-system`

С `agent-system` не стоит смешивать:

- конкретную reusable роль вроде `agent-role`;
- project-level selector `primary-agent-system`;
- runtime materialization state;
- один конкретный installed file или config artifact.

`Agent-system` — это класс target environments, а не конкретный role asset и не конкретный materialized output.

## 8. Naming conventions

Для этого concept используются разные surface forms в разных naming domains:

- human-facing term: `agent-system`;
- filesystem namespace: `agent_systems/`;
- possible Python class: `AgentSystem`.

Это согласованное отображение одного и того же concept, а не разные сущности.

## 9. Связанные термины

`agent-system` нужно читать вместе с:

- `primary-agent-system`;
- `agent-role`;
- `Runtime Materialization State`;
- `Project Portable Intent`.

Этот термин нужен для multi-agent architecture слоя `Project Methodology Runtime`.
