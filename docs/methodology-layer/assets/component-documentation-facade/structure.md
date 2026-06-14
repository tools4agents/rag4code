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
  operational_index.md      # quick operational facade route
  index.md                  # full stable documentation map
  develop_index.md          # create when development-only artifacts exist

  operational-guide.md
  service-contract.md       # for HTTP/service components
  cli-contract.md           # for CLI-oriented components
  api-contract.md           # for library/package APIs
  config-and-env.md         # for config, env and Secret Reference behavior
  integration-usage.md      # for runner/orchestrator/adjacent component usage

  develop/
    active_focus.md
    discussions/
      open_questions.md
      <historical-discussion>.md

  design/
  adr/
```

Not every component needs every file. Create focused docs when the component exposes that operational surface. Create `develop_index.md` and `docs/develop/` only when the component has development-only state or discussion history.

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

README should route by intent:

```text
docs/operational_index.md
  quick operational onboarding

docs/index.md
  full stable component documentation map

docs/develop_index.md
  development-only route, when development-only artifacts exist
```

README may also link to [`operational-guide.md`](#docsoperational-guidemd-role) or the most important contracts when that improves immediate navigation, but route selection should remain clear.

README should not contain all contracts, all config shapes, all design rationale or long troubleshooting history.

## docs/operational_index.md role

`docs/operational_index.md` is the quick operational facade route.

It answers:

```text
Which small set of docs should I read to understand and use this component now?
```

It should route to `docs/operational-guide.md` and the few focused docs needed for ordinary use: CLI/API/service contract, config/env, evidence/output and integration usage.

It should not route directly to development-only artifacts under `docs/develop/`.

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

`docs/index.md` may link to `docs/develop_index.md` as a clearly separated development-only route, but should not inline current focus, unresolved question lists or historical discussion summaries.

## docs/develop_index.md role

`docs/develop_index.md` is the development-only route.

It answers:

```text
How do I continue development, and where are current focus, open questions and historical discussion notes?
```

Create it when the component has current implementation handoff, unresolved questions or historical discussion artifacts.

It should route to:

```text
docs/develop/active_focus.md
docs/develop/discussions/open_questions.md
docs/develop/discussions/<historical-discussion>.md
stable contracts required before behavior changes
```

Development-only artifacts should stay under `docs/develop/` so they do not mix with stable component docs.

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

Development-only handoff and discussion docs are different from stable design/ADR docs. Keep temporary state and unresolved questions under `docs/develop/`; promote stabilized decisions into stable focused docs, design docs or ADRs.

## Source code orientation

The facade should make source code loading selective.

Good source-code policy in component docs:

```text
Use the facade for orientation and operational usage.
Read source code when changing behavior, debugging implementation, resolving ambiguity or verifying edge cases.
```

Do not write docs as if source code reading is forbidden. The goal is to avoid source-first discovery as the default onboarding path.

## Creation workflow

### Step 0 — component draft without operational facade

If a component source is only a draft, skeleton or development placeholder and does not yet expose stable operational usage, start with a development-only pre-facade:

```text
README.md
docs/develop_index.md
docs/develop/active_focus.md
```

Use this route when:

```text
component cannot be safely used as an operational unit yet;
CLI/API/service contracts are not stable;
integration behavior is still being designed;
the main need is to hand off current development focus and project-level context to agents.
```

`README.md` should briefly describe the intended component role, current maturity and where to read next. `docs/develop_index.md` should route to development-only state and to stable project-level Source of Truth docs required before implementation. `docs/develop/active_focus.md` should describe current implementation focus, immediate next steps, open assumptions and relevant links.

Do not create `docs/operational_index.md` or `docs/operational-guide.md` at this step unless there is a real operational surface to document. A fake operational facade makes unfinished behavior look stable.

### Step 1 — operational facade for usable components

When a component exposes a usable CLI, service, package API, adapter contract or integration route, create the operational facade:

```text
README.md
docs/operational_index.md
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

Add `docs/develop_index.md` and `docs/develop/` when there are development-only artifacts such as active focus, open questions or historical discussion notes.

When creating or updating multiple related docs, use [`batched-artifact-generation`](../batched-artifact-generation/SKILL.md).

## Consistency checklist

Before finishing, check:

- README routes instead of becoming a full manual;
- component drafts without stable operational usage use the pre-facade development route instead of fake operational docs;
- `operational_index.md` routes only to quick operational/stable usage docs;
- `operational-guide.md` remains the fast operational path;
- `docs/index.md`, if present, is a full map rather than another quickstart;
- `develop_index.md`, if present, is the only route to development-only artifacts;
- operational facade does not link directly to `docs/develop/active_focus.md`, `docs/develop/discussions/open_questions.md` or historical discussions;
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
- fake `operational-guide.md` for a component draft that cannot yet be safely used;
- one `usage.md` containing service contract, config, ADRs and integration history;
- operational facade linking directly to active focus, open questions or historical discussion notes;
- `docs/index.md` becoming a development handoff instead of stable documentation map;
- duplicating full contract examples across many docs without local need;
- hiding operational assumptions only in tests;
- making `docs/index.md` the operational guide after the documentation tree grows.

## Related docs

- [`index.md`](./index.md)
- [`SKILL.md`](./SKILL.md)
- [`entry-points.md`](./entry-points.md)
- [`rationale.md`](./rationale.md)
- [`batched-artifact-generation`](../batched-artifact-generation/index.md)
