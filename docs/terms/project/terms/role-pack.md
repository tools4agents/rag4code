# role-pack

> Status: Draft  
> Scope: project-specific term for HyperGraph artifact packaging model  
> Related: `docs/terms/index.md`

## 1. Назначение термина

`role-pack` — это reusable packaging unit для одной `agent-role`, которая объединяет связанные artifacts этой role unit без смешения их semantic boundaries.

## 2. Зачем нужен этот термин

Термин нужен, чтобы отделить:

- reusable role identity;
- packaging boundary для связанных artifacts;
- runtime materialization в конкретной `agent-system`.

Без этого distinction легко спутать:

- саму `agent-role`;
- abstract role artifact;
- `agent-system`-specific role assets;
- installed runtime files.

## 3. Что может входить в `role-pack`

В `role-pack` могут входить:

- abstract core role artifact;
- `agent-system`-specific assets;
- human-readable docs;
- metadata и support artifacts.

Это относится именно к `role-pack`, потому что `agent-role` по своей природе требует separate reusable core и system-specific representations.

Для `agent-system-agnostic asset` packs действует другой invariant:

- если pack является agnostic-layer pack, он не должен содержать внутри себя `agent-system`-specific assets.

Типичный пример:

```text
agent_roles/
  critic/
    role.md
    agent_systems/
      kilo/
        role.md
```

## 4. Важный invariant

`Role-pack` является packaging boundary, но не semantic collapse.

Это значит:

- файлы могут лежать рядом внутри одного pack;
- но abstract role artifact и `agent-system`-specific asset остаются разными artifacts;
- physical proximity не отменяет логических границ.

## 5. Что не стоит смешивать с `role-pack`

С `role-pack` не стоит смешивать:

- сам термин `agent-role`;
- конкретную `agent-system`;
- runtime materialization state;
- project-specific selection of role usage.

## 6. Связанные термины

`role-pack` нужно читать вместе с:

- `agent-role`;
- `agent-system`;
- `agent-system-agnostic asset`;
- `agent-system-specific asset`;
- `agent-system materialization`.

Этот термин нужен для artifact-oriented packaging model в HyperGraph.
