# Change Log - 2026-06-27 - Repository Agent Guidance

## Task

Create `AGENTS.md` in the repository root.

## Changes Applied

- Added `AGENTS.md` with repository-specific guidance for the Codex custom-agent catalog.
- Documented file scope, documentation rules, validation expectations, and change-log requirements.
- Updated `.gitignore` to allow `AGENTS.md` to be tracked.

## Reasoning

The repository needs durable guidance so future agent work preserves the catalog structure, avoids local path leakage in documentation, keeps agent metadata intact, and records all changes under `docs/`.

## Validation

- Confirmed `AGENTS.md` did not exist before creation.
- Updated `.gitignore` without adding any path pattern that starts with a dot.
- No Python or Rust source files were changed, so Pyright and `cargo check` were not applicable.
