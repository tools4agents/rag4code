# primary-agent-system

> Status: Draft  
> Scope: project-specific term for HyperGraph project intent and runtime selection  
> Related: `docs/terms/index.md`

## 1. Назначение термина

`primary-agent-system` — это выбранная разработчиком для работы с конкретным проектом основная `agent-system`, под которую HyperGraph должен materialize project runtime и related environment-facing assets.

## 2. Зачем нужен этот термин

Проект может использовать reusable assets, не завязанные на одну runtime platform и не привязанные навсегда к одной `agent-system`.

Поэтому нужен отдельный project-level selector, который отвечает на вопрос:

- какая именно `agent-system` считается основной execution environment для конкретного разработчика в этом проекте сейчас.

Без такого термина и selector concept трудно явно объяснить:

- почему materialized runtime выглядит именно так;
- почему выбраны конкретные `agent-system`-specific assets;
- почему в текущем developer context выбран один target runtime, хотя архитектурно допускается несколько systems.

## 3. Что означает `primary-agent-system`

`Primary-agent-system` задает:

- главную target environment для текущего developer-specific runtime в проекте;
- preferred target для выбора `agent-system`-specific assets;
- основу для runtime materialization policy внутри проекта.

Он не означает, что:

- другие `agent-system` больше не поддерживаются архитектурно;
- все assets проекта обязаны быть жестко завязаны на одну систему;
- все разработчики проекта обязаны использовать одну и ту же `agent-system`;
- reusable abstract assets теряют переносимость.

## 4. Связь с изоляцией настроек разработчика

На практике для одного и того же проекта могут существовать разные developer-specific runtime contexts:

- один разработчик работает через Kilo;
- другой — через Cursor.

При этом хорошей практикой считается, что настройки конкретной `agent-system` живут изолированно и не загрязняют основной project repo.

Например:

- developer-specific runtime files могут жить в nested git repo;
- основной проект сохраняет переносимые assets и intent;
- `agent-system`-specific runtime settings остаются локальными для того разработчика, которому они нужны.

Публикация таких настроек в основной репозиторий теоретически возможна, но обычно является анти-паттерном, если она начинает засорять project-level SoT или навязывать всем участникам одну agent environment.

## 5. Где фиксируется выбор

На уровне project configuration этот выбор должен фиксироваться через поле `primary_agent_system`.

То есть:

- `primary-agent-system` — human-facing domain term;
- `primary_agent_system` — config field, в котором этот выбор хранится.

Это одно и то же concept в разных naming domains.

## 6. Связь с materialization

`Primary-agent-system` влияет на то, как HyperGraph materialize runtime в проекте:

- какие `agent-system`-specific assets считать релевантными;
- какой runtime-facing layout готовить;
- какие environment-specific artifacts должны появиться в project-scoped runtime.

При этом сам selector не является materialized runtime artifact. Он является частью project intent.

## 7. Связь с другими слоями

`Primary-agent-system` относится к `Project Portable Intent`, а не к reusable catalog layer.

Это значит:

- reusable methodology или role pack не обязаны сами по себе определять primary system;
- developer working context выбирает primary system как часть своей проектной конфигурации;
- runtime materialization затем использует этот выбор как selector.

## 8. Что не стоит смешивать с `primary-agent-system`

С `primary-agent-system` не стоит смешивать:

- сам термин `agent-system` как класс target environments;
- конкретный `agent-role`;
- runtime materialization state;
- installed runtime files;
- adapter-specific asset как source artifact.

`Primary-agent-system` — это selector внутри project intent, а не отдельный runtime artifact.

## 9. Naming conventions

Для этого concept используются разные surface forms:

- human-facing term: `primary-agent-system`;
- config field: `primary_agent_system`;
- possible Python field: `primary_agent_system`.

## 10. Связанные термины

`primary-agent-system` нужно читать вместе с:

- `agent-system`;
- `Project Portable Intent`;
- `Runtime Materialization State`;
- `project-scoped runtime`.

Этот термин нужен, чтобы явно отделять reusable architecture от project-specific runtime target selection.
