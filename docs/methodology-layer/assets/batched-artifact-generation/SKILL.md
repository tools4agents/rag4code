---
name: batched-artifact-generation
description: Use mini-batches when creating or updating many related markdown artifacts to preserve focus, consistency and navigability.
version: 1.0.0
---

# Skill: Batched Artifact Generation

## When to use

Use this skill when asked to create or update many related artifacts, especially:

- 10+ markdown files;
- 3+ conceptually distinct document groups;
- term pages plus focused docs;
- contracts plus examples;
- documentation requiring index/navigation synchronization.

## Operating rule

Do not create all artifacts at once before structure and batch plan are accepted.

Use this workflow:

```text
1. Propose structure.
2. Wait for human approval or corrections.
3. Propose mini-batch plan.
4. Wait for human approval or corrections.
5. Execute approved batches using selected execution mode.
6. Summarize created/updated files after each batch.
7. Run final consistency pass.
```

## Interaction model

For semantic artifact generation, work interactively by default.

Do not start creating many files before the structure and batch plan are accepted, unless the user explicitly asks for autonomous execution.

Human checkpoints:

```text
1. Structure and file roles approved.
2. Batch plan approved.
3. Semantic batch reviewed or accepted.
4. Final consistency pass completed.
```

## Execution modes

### Step-by-step mode

Default for semantic docs, architecture docs, term pages, contracts and plans.

Process:

```text
1. Execute one approved batch.
2. Summarize created/updated files and captured decisions.
3. Wait for human review, corrections or approval.
4. Continue only after user confirmation.
```

### Continuous mode

Use only when the user explicitly asks to continue through all batches, or when the work is mechanical after approval.

Process:

```text
1. Execute approved batches sequentially.
2. Summarize each batch.
3. Run final consistency pass.
4. Report final result.
```

## Batch size

Recommended batch size:

- 1–2 files for core architecture docs, ADRs or contract boundaries;
- 3–5 files for focused docs, term pages or plan artifacts;
- 5–10 files only for mechanical stubs/templates.

If files require semantic decisions, prefer smaller batches.

## Per-batch checklist

After each batch, check:

- files created or updated;
- local index/navigation updated;
- no duplicate definitions across term pages and focused docs;
- accepted terms are reused consistently;
- links use meaningful labels;
- next batch is clear.

## Final consistency pass

At the end, check:

- terminology consistency;
- navigation completeness;
- duplicate or competing definitions;
- term page vs focused spec boundaries;
- broken or awkward links;
- docs that should be split or merged;
- stale placeholders or planned files listed as completed.

## Why this helps

Batches reduce semantic drift, duplicated definitions, forgotten links and navigation gaps.

This is not only an LLM limitation. It is engineering control for large relational documentation changes.
