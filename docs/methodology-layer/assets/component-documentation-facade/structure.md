# Structure for Component Documentation Facade

> Status: Draft  
> Scope: methodology-layer assets  
> Role: practical structure guide for component-local documentation facades

## Purpose

This document describes the recommended file structure and file roles for a `Component Documentation Facade`.

Use it when creating or refactoring component-local docs so the component can be understood through a facade before source-first discovery.

## Recommended structure

```text
README.md
docs/
  operational-guide.md
  index.md                  # create when full documentation map is needed
  service-contract.md       # for HTTP/service components
  cli-contract.md           # for CLI-oriented components
  api-contract.md           # for library/package APIs
  config-and-env.md         # for config, env and Secret Reference behavior
  integration-usage.md      # for runner/orchestrator/adjacent component usage
  design/
  adr/
```

Not every component needs every file. Create focused docs when the component exposes that operational surface.

## README.md role

`README.md` is the top-level routing surface, not the full manual.

Recommended sections:

```text
# <component-name>
short purpose
when to use
quick start or minimal usage
Documentation entry point
Where to go next
commands
boundary
```

README should link to:

- [`operational-guide.md`](#docsoperational-guidemd-role) for quick operational onboarding;
- `docs/index.md` when a full documentation map exists;
- the most important focused docs if that helps immediate navigation.

README should not contain all contracts, all config shapes, all design rationale or long troubleshooting history.

## docs/operational-guide.md role

`docs/operational-guide.md` is the fast operational path.

It answers:

```text
How do I quickly understand and use this component safely?
```

Recommended sections:

```text
Purpose
When to use
Quick start
Minimal verification
Primary contract links
Config/env summary
Common integration path
Boundary
Where to go next
```

The operational guide can repeat small examples from focused docs when that improves local usability, but it should not become the full documentation map or design history.

## docs/index.md role

`docs/index.md` is the full component documentation map.

It answers:

```text
What documentation exists for this component?
Where are the entry points or Source of Truth for each topic?
```

Create `docs/index.md` when component docs include materials that should not be loaded through `operational-guide.md`, for example:

- ADRs;
- design notes;
- rationale docs;
- evidence docs;
- multiple contracts;
- test documentation;
- migration or compatibility notes.

A small component may start without `docs/index.md`. Add it when `operational-guide.md` would otherwise become a mixed navigation map.

## Focused operational docs

Focused docs should each describe one bounded operational context.

Common patterns:

```text
service-contract.md
  service launch route, endpoints, health semantics, request/response examples

cli-contract.md
  commands, arguments, outputs, exit codes

api-contract.md
  package API surface, callable behavior, stable examples

config-and-env.md
  config shape, env vars, Secret References, redaction and materialization rules

integration-usage.md
  how adjacent runtime, runner, orchestrator or adapter components should use this component
```

Use component-specific names when they are clearer, for example:

```text
process-runtime-usage.md
adapter-contract.md
backend-config.md
storage-semantics.md
```

## Design and decision docs

Design docs, ADRs and rationale docs should stay outside the operational facade path unless they are needed for the current task.

Typical locations:

```text
docs/design/
docs/adr/
docs/rationale.md
```

These docs answer:

```text
Why does this component exist?
Why is it designed this way?
Which alternatives were rejected?
Which trade-offs were accepted?
```

Operational docs may link to them, but should not duplicate their reasoning.

## Source code orientation

The facade should make source code loading selective.

Good source-code policy in component docs:

```text
Use the facade for orientation and operational usage.
Read source code when changing behavior, debugging implementation, resolving ambiguity or verifying edge cases.
```

Do not write docs as if source code reading is forbidden. The goal is to avoid source-first discovery as the default onboarding path.

## Creation workflow

For a new component, start with:

```text
README.md
docs/operational-guide.md
```

Then add focused docs for exposed surfaces:

```text
service contract
CLI contract
API contract
config/env behavior
integration usage
```

Add `docs/index.md` when the documentation set grows beyond the operational facade.

When creating or updating multiple related docs, use [`batched-artifact-generation`](../batched-artifact-generation/SKILL.md).

## Consistency checklist

Before finishing, check:

- README routes instead of becoming a full manual;
- `operational-guide.md` remains the fast operational path;
- `docs/index.md`, if present, is a full map rather than another quickstart;
- focused docs have one bounded context each;
- operational docs do not absorb ADR/design/rationale material;
- examples are runnable or clearly marked as candidate/intended;
- config/env docs distinguish real secret handling from fixture/test values;
- links have meaningful labels;
- source code is positioned as deeper context, not default discovery.

## Anti-patterns

Avoid:

- `index_fast.md` or other names that describe speed rather than document role;
- README as a dumping ground for every example;
- one `usage.md` containing service contract, config, ADRs and integration history;
- duplicating full contract examples across many docs without local need;
- hiding operational assumptions only in tests;
- making `docs/index.md` the operational guide after the documentation tree grows.

## Related docs

- [`index.md`](./index.md)
- [`SKILL.md`](./SKILL.md)
- [`rationale.md`](./rationale.md)
- [`batched-artifact-generation`](../batched-artifact-generation/index.md)
