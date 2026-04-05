# Technical Context

## Core Stack

- Primary language: Python 3.13+
- Package manager: `uv`
- Orchestration: HSM

## Main Technical Areas

- `services/` contains service-level components and MCP-oriented tools.
- `hsm/` contains orchestration logic for stack management.
- `docs/` contains long-lived engineering documentation and contracts.

## Environment Assumptions

- Primary development environment: Linux
- Repository layout includes nested git repositories.
- Documentation and machine-readable contracts are treated as first-class engineering artifacts.

## External Dependencies

- Docker is used for containerized workflows and environment orchestration.
- Service-specific dependencies are defined in component-level manifests such as `pyproject.toml` files.

## Important Technical Conventions

- New code should respect the Python and `uv`-based project baseline.
- Comments, docstrings, and identifiers in code should remain in English.
- Commit messages should remain in English.

## Related Source Of Truth

- Project values: `docs/principles.md`
- Methodology runtime overview: `docs/methodology-layer/overview.md`
- Contracts layer policy: `docs/contracts/README.md`
