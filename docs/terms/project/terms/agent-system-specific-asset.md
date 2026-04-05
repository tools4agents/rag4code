# agent-system-specific asset

> Status: Draft  
> Scope: project-specific term for HyperGraph asset classification  
> Related: `docs/terms/terms_map.md`

## 1. Назначение термина

`Agent-system-specific asset` — это asset, совместимый с конкретной `agent-system` на уровне представляемого артефакта и используемый как source layer для соответствующего runtime target.

## 2. Зачем нужен этот термин

Термин нужен, чтобы отделить:

- abstract reusable assets;
- authored or maintained assets под конкретную `agent-system`;
- runtime materialization outputs.

Важно, что `agent-system-specific asset` не обязан быть автоматически сгенерирован. Он может быть создан и поддерживаться вручную.

## 3. Типичные примеры

Примеры `agent-system-specific asset`:

- `agent_roles/critic/agent_systems/kilo/role.md`;
- другие source artifacts, подготовленные под model constraints конкретной `agent-system`.

## 4. Связь с reusable source layer

`Agent-system-specific asset` обычно связан с reusable abstract asset, но не подменяет его.

Например:

- abstract `agent-role` задает reusable semantics;
- `agent-system`-specific role asset задает representation для выбранной system;
- runtime materialization затем уже раскладывает environment-facing files в проекте.

## 5. Что не стоит смешивать с `agent-system-specific asset`

С этим термином не стоит смешивать:

- abstract reusable artifact;
- runtime materialization state;
- installed runtime file как конечный output.

## 6. Связанные термины

`Agent-system-specific asset` нужно читать вместе с:

- `agent-system`;
- `agent-system-agnostic asset`;
- `role-pack`;
- `agent-system materialization`.
