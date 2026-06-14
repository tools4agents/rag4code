---
name: component-documentation-facade
description: Create a lazy-loading documentation facade for component sources so humans and agents can use components without source-first discovery.
version: 1.0.0
---

# Skill: Component Documentation Facade

## When to use

Use this skill when creating or updating documentation for a component source, especially when the component:

- exposes a CLI, HTTP service, package API, adapter contract or integration route;
- will be used by other developers, agents, contributors or integration tests;
- needs quick operational onboarding without reading source code first;
- has or will have design docs, ADRs, rationale docs or evidence that should not be mixed into quick usage docs.

## Goal

Create a documentation facade that lets a human or agent answer quickly:

```text
What is this component?
When should I use it?
How do I run it or call it?
What operational contract does it expose?
What config/env inputs matter?
How is it used by adjacent runtime/runner/orchestrator layers?
Where should I go next?
```

## Default structure

Recommended component-local structure:

```text
README.md
docs/
  operational_index.md
  index.md                  # full stable documentation map
  develop_index.md          # add when development-only artifacts exist

  operational-guide.md
  <focused-operational-doc>.md
  <config-or-contract-doc>.md
  <integration-usage-doc>.md

  develop/
    active_focus.md
    discussions/
      open_questions.md
      <historical-discussion>.md
```

`README.md` should be a compact intent router.

`docs/operational_index.md` should be the quick operational facade route.

`docs/operational-guide.md` should be the fast operational path.

`docs/index.md` should be the full stable documentation map when component docs grow beyond the operational facade.

`docs/develop_index.md` should be the development-only route when active focus, open questions or historical discussion notes exist.

For detailed file roles, recommended sections and naming patterns, use [`structure.md`](./structure.md) and [`entry-points.md`](./entry-points.md).

## Source code policy

Orient by the documentation facade first.

Read source code when the task requires:

- behavior changes;
- debugging implementation;
- ambiguity resolution;
- undocumented edge cases;
- implementation verification.

Do not treat source-first discovery as the default way to understand how to use a component.

## Facade vs design documentation

Keep these documentation layers separate:

```text
Documentation facade
  answers: how do I understand and use this component safely?

Design / ADR / rationale docs
  answer: why does this component exist and why is it designed this way?
```

Operational facade docs may link to design docs, but should not become design-history documents.

## Entry point separation

Keep three reader intents separate:

```text
docs/operational_index.md
  quick usage and operational onboarding

docs/index.md
  full stable documentation map

docs/develop_index.md
  current development state, open questions and history
```

Operational facade must not link directly to development-only artifacts under `docs/develop/`.

## Batch workflow

If creating or updating the facade requires multiple related markdown files, use [`batched-artifact-generation`](../batched-artifact-generation/SKILL.md).

Recommended sequence:

```text
1. Propose facade structure and file roles.
2. Create README.md as top-level intent router.
3. Create docs/operational_index.md and docs/operational-guide.md.
4. Add focused operational docs.
5. Add docs/index.md when there is documentation beyond the operational facade.
6. Add docs/develop_index.md and docs/develop/ only when development-only artifacts exist.
7. Run final consistency pass for navigation, duplication and layer boundaries.
```

## Final consistency pass

Check that:

- README routes instead of becoming a full manual;
- `operational_index.md` is the quick operational facade route;
- `operational-guide.md` is the fast operational path;
- `docs/index.md`, if present, is a full stable documentation map;
- `develop_index.md`, if present, is the only route to development-only artifacts;
- operational docs do not link directly to `docs/develop/active_focus.md`, `docs/develop/discussions/open_questions.md` or historical discussion notes;
- focused docs have one bounded context each;
- design/ADR/rationale content is not mixed into quick usage docs;
- links have meaningful labels;
- source code is referenced as deeper context, not default orientation.

## Anti-patterns

Avoid:

- using source code as the default component discovery layer;
- turning README into a monolithic manual;
- using `docs/index.md` as both fast guide and full documentation map after docs grow;
- using `docs/index.md` as active development handoff;
- mixing quick usage, ADR rationale and implementation internals in one document;
- leaking active focus, open questions or historical discussions into operational facade;
- duplicating full examples across many files without local need;
- forbidding source code reading when the task actually requires it.
