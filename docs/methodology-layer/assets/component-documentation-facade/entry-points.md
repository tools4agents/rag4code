# Entry Points for Component Documentation Facade

> Status: Draft  
> Scope: methodology-layer assets  
> Role: intent-based entry point model for component-local documentation

## Purpose

This document fixes the intent-based entry point model for component source documentation.

Component documentation should separate three reader intents:

```text
I want to quickly understand what this component is and how to use it.
I want to study the full stable component documentation map.
I want to continue development and see current focus, open questions and history.
```

One index file should not serve all three intents at once.

## Entry point model

Recommended top-level routing:

```text
README.md
  -> docs/operational_index.md
       quick operational facade

  -> docs/index.md
       full stable component documentation map

  -> docs/develop_index.md
       development-only route, when development-only artifacts exist
```

`README.md` is the top-level intent router. It should help the reader choose the correct route, not become a complete manual.

## `docs/operational_index.md`

`docs/operational_index.md` answers:

```text
How do I quickly understand and use this component safely?
```

It routes to:

- `docs/operational-guide.md`;
- primary CLI/API/service contract docs;
- config/env docs needed for quick use;
- evidence/output docs needed to read results;
- integration usage docs when adjacent component usage is part of ordinary operation.

It must not route directly to development-only artifacts such as:

```text
docs/develop/active_focus.md
docs/develop/discussions/open_questions.md
docs/develop/discussions/<historical-discussion>.md
```

Operational facade must not leak development state.

## `docs/index.md`

`docs/index.md` answers:

```text
What stable documentation exists for this component, and where is the Source of Truth for each topic?
```

It is the full stable component documentation map.

It may route to:

- operational entry points;
- component-local contracts;
- config/env docs;
- integration usage docs;
- design, ADR, rationale or test docs;
- `docs/develop_index.md` as a clearly separated development-only route.

It should not inline active development state, unresolved question lists or historical discussion summaries.

## `docs/develop_index.md`

`docs/develop_index.md` answers:

```text
How do I continue development, and where are current focus, open questions and historical discussion notes?
```

Create it when the component has development-only artifacts.

It routes to:

- `docs/develop/active_focus.md`;
- `docs/develop/discussions/open_questions.md`;
- historical discussion outcomes;
- stable component contracts that must be read before behavior changes.

Development-only artifacts may contain temporary state, unresolved questions and handoff notes. Once a decision stabilizes, promote it to stable focused docs and keep `develop/` as handoff/history, not canonical contract storage.

## Routing invariant

Use this rule:

```text
README.md chooses the route.
Index files route.
Focused docs define.
Development docs hand off current state and history.
```

Do not duplicate full schemas, contract examples or open question text across index files.

## Source code policy

The entry point model makes source code loading selective. It does not forbid source code reading.

Read source code when changing behavior, debugging implementation, resolving ambiguity, investigating undocumented edge cases or verifying implementation details.
