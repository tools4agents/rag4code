# Batched Artifact Generation

> Status: Draft  
> Scope: methodology-layer assets  
> Role: навигация по practice безопасного создания множества связанных artifacts

## Назначение

Этот asset фиксирует practice для задач, где агент должен создать или обновить много связанных markdown artifacts: docs, term pages, contracts, templates, plans or indexes.

Practice нужна, чтобы сохранить semantic consistency, не потерять навигацию и не смешать роли документов при большой генерации.

## Core formula

```text
Structure first
  -> batch plan
    -> execute small batches
      -> update navigation
        -> final consistency pass
```

## Когда использовать

Используй этот pattern, если задача включает:

- 10+ markdown files;
- 3+ conceptually distinct document groups;
- term pages plus focused docs;
- contracts plus examples;
- high risk of terminology drift or duplicated definitions.

## Files

- [`SKILL.md`](./SKILL.md) — короткая operational instruction для агента.
- [`rationale.md`](./rationale.md) — подробное объяснение, почему batch workflow лучше для крупных artifact-generation задач.

## Boundary

Этот asset не задает конкретный project layout и не заменяет project-local documentation rules.

Он фиксирует общий execution pattern для больших documentation/materialization changes.
