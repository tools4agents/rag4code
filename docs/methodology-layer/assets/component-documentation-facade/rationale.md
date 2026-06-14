# Rationale for Component Documentation Facade

> Status: Draft  
> Scope: methodology-layer assets  
> Role: explanation of why component sources need a facade-first documentation layer

## Problem

Source-first component discovery does not scale.

It works for one small package because an agent or developer can inspect source code, configs and tests directly. It breaks when a workspace has many component sources, each with its own runtime route, configs, env handling, contracts, tests and integration semantics.

Typical failure modes:

- context windows are spent on implementation details before the component role is understood;
- agents infer usage from code paths that were not intended as public or operational contracts;
- README files become either too small to be useful or too large to navigate;
- operational usage, design rationale and ADR history get mixed in one document;
- quick usage, full stable documentation map and active development handoff collapse into one overloaded index;
- unresolved questions leak into operational onboarding and look like stable component behavior;
- contributors cannot tell which docs are for using the component and which docs explain why it was designed that way;
- integration tests duplicate undocumented assumptions about launch commands, env names, ports or health endpoints.

## Why a facade helps

A `Component Documentation Facade` creates a stable first orientation layer.

It lets a human or agent answer operational questions before reading source code:

```text
What is this component?
When should I use it?
How do I launch it?
What contract does it expose?
Which config/env inputs matter?
How does another runtime or runner component use it?
Where should I go next?
```

This preserves source code as implementation truth while avoiding source code as the default discovery interface.

## Facade vs source code

The facade is not a source-code replacement.

Correct relationship:

```text
documentation facade
  first orientation and operational contract layer

source code
  implementation truth and deeper verification layer
```

Read source code when the task requires behavior changes, debugging, ambiguity resolution, undocumented edge cases or implementation verification.

Do not require source code reading just to learn how to run or integrate a component.

## Facade vs design documentation

Operational facade docs and design docs answer different questions.

```text
Documentation facade
  How do I understand and use this component safely?

Design / ADR / rationale docs
  Why does this component exist and why is it designed this way?
```

If these layers are mixed, quick operational onboarding becomes too expensive, and design reasoning becomes harder to find.

The facade may link to design docs, ADRs and rationale, but it should not become a design-history document.

## Why `operational-guide.md` is separate from `docs/index.md`

`docs/operational-guide.md` is the fast operational path.

It should answer:

```text
How do I quickly understand and use this component?
```

`docs/index.md` is the full documentation map.

It should answer:

```text
What documentation exists for this component, and where are the entry points or Source of Truth for each topic?
```

A small component may not need `docs/index.md` at first. When docs grow to include ADRs, design notes, rationale, evidence, multiple contracts or test documentation, `docs/index.md` becomes necessary so `operational-guide.md` can stay focused.

## Why component docs need intent-based entry points

Component readers arrive with different intents.

```text
Use the component now.
Understand the full stable documentation map.
Continue development from current handoff state.
```

If one file tries to serve all three intents, it becomes semantically unstable:

- operational onboarding is polluted by unresolved implementation questions;
- stable documentation maps start carrying temporary active-focus state;
- development handoff starts looking like canonical behavior;
- agents load more context than the current task requires.

The entry point split prevents this:

```text
README.md
  top-level intent router

docs/operational_index.md
  quick operational facade

docs/index.md
  full stable component documentation map

docs/develop_index.md
  development-only route, when current development state exists
```

The key invariant is:

```text
Operational facade must not leak development state.
```

Active focus, open questions and historical discussion notes should live under `docs/develop/` and be routed through `docs/develop_index.md`, not through the operational facade.

## Why README should route, not contain everything

README is the public top-level entry point of the component source.

Its job is to route quickly:

```text
purpose
when to use
minimal quick start
documentation entry point
where to go next
commands
boundary
```

If README becomes the full manual, it starts competing with focused docs and loses navigability.

If README is too small, agents fall back to source-first discovery.

A good README gives enough orientation to choose the next document.

With intent-based routing, README should route to the appropriate entry point instead of forcing every reader through the same path.

## Why this matters for agents

Agents need lazy-loading documentation more than humans do.

A human can skim a repository visually. An agent must load text into a finite context window. Without a facade, the agent often reads source code, tests and configs to reconstruct operational usage. That approach is slow, brittle and expensive when the workspace contains many components.

A facade-first pattern lets the agent load:

```text
README.md
  -> docs/operational_index.md
       -> docs/operational-guide.md
       -> one focused doc for the current question
```

Source code is loaded when the operational layer is insufficient for the task.

## Good result

A component with a good documentation facade allows a new agent or contributor to:

- identify the component role without reading source code;
- run the component or understand why it cannot be run standalone;
- find its operational contract;
- find config/env requirements;
- understand integration boundaries;
- distinguish quick usage docs from design/ADR/rationale docs;
- distinguish operational, stable-map and development-only routes;
- know when source code reading is appropriate.

## Anti-patterns

Avoid:

- source-first discovery as the normal component onboarding path;
- README as a monolithic manual;
- `docs/index.md` as both quickstart and full documentation map after docs grow;
- `docs/index.md` as active development handoff;
- operational facade linking directly to active focus, open questions or historical discussions;
- ADR/design rationale embedded into operational quick-use docs;
- operational assumptions encoded only in tests;
- source-code reading bans that prevent necessary debugging or verification.

## Related docs

- [`index.md`](./index.md)
- [`SKILL.md`](./SKILL.md)
- [`entry-points.md`](./entry-points.md)
- [`batched-artifact-generation`](../batched-artifact-generation/index.md)
