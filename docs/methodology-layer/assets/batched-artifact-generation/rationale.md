# Rationale for Batched Artifact Generation

> Status: Draft  
> Scope: methodology-layer assets  
> Role: explanation of why large artifact-generation tasks should be done in mini-batches

## Problem

When an agent creates many related artifacts at once, the main risk is not syntax. The main risk is semantic drift.

Typical failure modes:

- inconsistent terminology;
- duplicated definitions;
- focused docs and term pages repeating each other;
- navigation/index files lagging behind created files;
- files with unclear roles;
- hidden gaps masked by apparent completeness;
- overlong files that should have been split;
- stale planned links;
- one file silently changing the model established by another file.

## Why batching works

Batched generation gives local control over a large relational change.

It allows the agent and human reviewer to verify after each small unit:

```text
Does this batch preserve the intended model?
Do new files have clear roles?
Are links and navigation still correct?
Did any file duplicate another file's responsibility?
```

## Recommended workflow

```text
Structure proposal
  -> batch plan
    -> batch execution
      -> batch summary
        -> final consistency pass
```

### Structure proposal

Before writing files, define:

- folder layout;
- file names;
- role of each file;
- reading order;
- which files are term pages, focused docs, templates or indexes.

### Batch plan

Group files by semantic locality:

- navigation and overview;
- core focused specs;
- term pages;
- templates/examples;
- synchronization and final pass.

### Batch execution

Create or update one batch at a time.

Keep batch size small enough that the agent can maintain a consistent local model.

### Batch summary

After each batch, summarize:

- created files;
- updated files;
- decisions captured;
- next batch.

### Final consistency pass

The final pass is mandatory for semantic work.

It catches cross-file inconsistencies that are invisible inside one batch.

## Batch sizing

Suggested sizes:

```text
1–2 files: core architecture, ADR, contract boundary.
3–5 files: focused docs, term pages, plans.
5–10 files: mechanical templates or stubs only.
```

If a file contains a core semantic decision, keep the batch smaller.

## Why this is not obsolete

Stronger models reduce some generation errors, but they do not remove the need for engineering control.

Large documentation systems are relational. A correct file can still be wrong if it conflicts with another file, duplicates a term page or breaks navigation.

Batching is therefore not just a workaround for model limitations. It is a documentation engineering practice.

## Anti-patterns

Avoid:

- generating 20–30 semantic files in one pass;
- skipping structure proposal;
- creating term pages and focused specs with duplicate definitions;
- updating files without navigation/index synchronization;
- treating generated completeness as semantic correctness;
- skipping final consistency pass.

## Good result

A good batched artifact-generation session leaves:

- clear folder structure;
- coherent file roles;
- updated navigation;
- consistent terminology;
- no obvious duplicate definitions;
- concise batch summaries;
- final consistency check result.
