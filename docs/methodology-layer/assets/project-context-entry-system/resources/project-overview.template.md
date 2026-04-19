# Project Overview

## Purpose

`<project-slug>` — <short project purpose>.

## Current Baseline

- primary runtime mode: <mode>
- stack baseline: <stack>
- current delivery phase: <phase>

## Context Layers

Проект использует layered context model:

- `AGENTS.md` как top-level router artifact;
- `project/` как durable project context;
- `docs/` как engineering Source of Truth;
- `operational_scope/` как temporary execution layer.

## Main Areas

- `project/` — durable project context.
- `docs/` — long-lived engineering documentation.
- `operational_scope/` — tasks и execution context.
