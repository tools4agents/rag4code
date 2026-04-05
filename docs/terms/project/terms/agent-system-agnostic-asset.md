# agent-system-agnostic asset

> Status: Draft  
> Scope: project-specific term for HyperGraph asset classification  
> Related: `docs/terms/terms_map.md`

## 1. Назначение термина

`Agent-system-agnostic asset` — это asset, который не зависит от конкретной `agent-system` и может использоваться как reusable source artifact до выбора runtime target.

Важный structural invariant:

- такой asset или pack не содержит внутри себя `agent-system`-specific assets;
- он используется как общий source layer сразу для всех `agent-system`.

## 2. Зачем нужен этот термин

Термин нужен, чтобы отделить:

- portable reusable source layer;
- `agent-system`-specific source layer;
- runtime materialization layer.

Без этого distinction система быстро начинает смешивать abstract semantics и environment-specific representations.

## 3. Типичные примеры

Типичными примерами `agent-system-agnostic asset` являются:

- methodology assets;
- abstract `agent-role` artifacts;
- governance artifacts;
- часть reusable rules и skills, если они не завязаны на одну `agent-system`.

## 4. Связь с project portability

Именно `agent-system-agnostic assets` позволяют проекту:

- не зависеть от одной coding agent system;
- поддерживать нескольких разработчиков с разными preferred environments;
- откладывать выбор runtime target до project- or developer-specific configuration.

## 5. Связь с pack structure

Если `agent-system-agnostic asset` поставляется как pack, такой pack должен оставаться чисто agnostic-layer unit.

Это значит:

- внутри него не должны лежать `agent-system`-specific assets;
- он не должен смешивать общий reusable source layer с system-specific representations;
- system-specific variants должны жить отдельно, в своей собственной family of assets или в separate pack structure.

## 6. Что не стоит смешивать с `agent-system-agnostic asset`

С этим термином не стоит смешивать:

- `agent-system`-specific assets;
- packs, внутри которых одновременно лежат agnostic и system-specific layers;
- installed runtime files;
- generated materialization outputs.

## 7. Связанные термины

`Agent-system-agnostic asset` нужно читать вместе с:

- `agent-system`;
- `agent-system-specific asset`;
- `agent-system materialization`;
- `Project Portable Intent`.
