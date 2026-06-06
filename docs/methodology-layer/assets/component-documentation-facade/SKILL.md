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
  operational-guide.md
  index.md                  # add when full documentation map is needed
  <focused-operational-doc>.md
  <config-or-contract-doc>.md
  <integration-usage-doc>.md
```

`README.md` should be a compact routing surface.

`docs/operational-guide.md` should be the fast operational path.

`docs/index.md` should be the full documentation map when component docs grow beyond the operational facade.

For detailed file roles, recommended sections and naming patterns, use [`structure.md`](./structure.md).

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

## Batch workflow

If creating or updating the facade requires multiple related markdown files, use [`batched-artifact-generation`](../batched-artifact-generation/SKILL.md).

Recommended sequence:

```text
1. Propose facade structure and file roles.
2. Create README.md and docs/operational-guide.md.
3. Add focused operational docs.
4. Add docs/index.md only when there is documentation beyond the operational facade.
5. Run final consistency pass for navigation, duplication and layer boundaries.
```

## Final consistency pass

Check that:

- README routes instead of becoming a full manual;
- `operational-guide.md` is the fast operational path;
- `docs/index.md`, if present, is a full documentation map;
- focused docs have one bounded context each;
- design/ADR/rationale content is not mixed into quick usage docs;
- links have meaningful labels;
- source code is referenced as deeper context, not default orientation.

## Anti-patterns

Avoid:

- using source code as the default component discovery layer;
- turning README into a monolithic manual;
- using `docs/index.md` as both fast guide and full documentation map after docs grow;
- mixing quick usage, ADR rationale and implementation internals in one document;
- duplicating full examples across many files without local need;
- forbidding source code reading when the task actually requires it.
