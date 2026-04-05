# Project Overview

## Purpose

HyperGraph is an open source project focused on building a unified knowledge graph across code, documentation, tasks, contracts, and methodology artifacts.

The project is designed for human and AI-agent collaboration and treats engineering knowledge as a first-class part of the system.

## High-Level Concept

HyperGraph is not a single monolith. It is an ecosystem of reusable services, project assets, and orchestration layers.

At a high level the repository combines:

- independent services and MCP-oriented components;
- orchestration through HSM;
- long-lived engineering documentation in `docs/`;
- evolving methodology artifacts for agent-enabled software delivery.

## Project Values

The current project baseline emphasizes:

- openness and reusability of engineering assets;
- clarity for both humans and agents;
- flexibility of methodology, workflows, and runtime projections;
- traceability between decisions, artifacts, and implementation.

Canonical project values are described in `docs/principles.md`.

## Context Layers

The repository is being migrated to a layered context model:

- `AGENTS.md` as the navigation contract;
- `project/` as durable project context;
- `docs/` as engineering Source of Truth;
- `operational_scope/` as temporary execution layer;
- `.kilo/` as Kilo-specific configuration and behavior layer.

## Main Areas

- `services/` for service-level implementation work;
- `hsm/` for orchestration and stack management;
- `docs/` for architecture, contracts, principles, and ADRs;
- `project/` for stable repository context;
- `operational_scope/` as the execution layer for the current iteration.
