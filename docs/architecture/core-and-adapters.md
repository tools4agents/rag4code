# Core and Adapters

> Status: Draft  
> Scope: architecture baseline for HyperGraph core and external interfaces  
> Role: internal responsibility boundaries for core, ports, CLI and MCP adapters

## Назначение

HyperGraph должен строиться как core-oriented system with thin adapters.

Core owns business logic. Interfaces expose that logic to humans and agents. No adapter should implement its own independent graph semantics, indexing rules or refactoring behavior.

## Baseline architecture

```text
CLI adapter
    -> application ports
        -> HyperGraph core
            -> storage port
            -> filesystem port
            -> parser/indexer services
MCP adapter
    -> application ports
        -> HyperGraph core
```

This structure keeps CLI and MCP behavior consistent because both interfaces call the same core capabilities.

## Core responsibilities

HyperGraph core owns:
- project-scoped operation semantics;
- graph query behavior;
- incoming/outgoing link logic;
- affected files calculation;
- impact report construction;
- move/rename planning;
- safe rewrite decision boundaries;
- reindex/rebuild orchestration;
- validation of root boundary constraints.

Core must not depend on a specific UI, CLI command shape or MCP transport details.

## Ports

Ports define what the core needs from external mechanisms.

Candidate ports:
- project registry port;
- project config port;
- filesystem port;
- storage port;
- parser/link extraction port;
- report rendering port.

Ports are architecture boundaries, not final implementation tasks.

## CLI adapter

CLI is a first-class interface for human operators.

CLI responsibilities:
- register/select project;
- trigger index/reindex/rebuild;
- run graph inspection commands;
- request move dry-run/apply;
- request remove impact report;
- render human-readable output.

CLI must not implement separate graph logic. It calls application ports/core use cases.

## MCP adapter

MCP is a first-class interface for AI agents.

MCP responsibilities:
- expose machine-readable project and graph operations;
- return structured impact reports;
- expose incoming/outgoing link queries;
- expose move planning/apply operations when safe;
- expose remove impact report without semantic text rewriting.

MCP must not implement separate graph logic. It calls the same core use cases as CLI.

## Shared operation model

CLI and MCP should expose the same conceptual operations even if their transport contracts differ.

Examples:
- `register_project`;
- `reindex_project`;
- `get_incoming_links`;
- `get_outgoing_links`;
- `get_remove_impact`;
- `plan_move_markdown_file`;
- `apply_move_markdown_file`.

Exact command names and contracts belong to later contract design.

## Excluded architecture directions

HyperGraph should not be built as:
- VSCode-first extension;
- IDE plugin with embedded business logic;
- MCP server with duplicated graph logic;
- CLI tool with duplicated graph logic;
- Markdown LSP-centered system for the Markdown MVP.

LSP may be reconsidered in future for programming language source code artifact extraction, but it is not part of the Markdown first-iteration architecture baseline.
