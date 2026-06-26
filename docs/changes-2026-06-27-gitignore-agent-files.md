# Change Log - 2026-06-27 - Agent-Focused Gitignore

## Task

Add a `.gitignore` that allows only files related to the agent repository and avoids ignore paths that start with a dot.

## Changes Applied

- Added a root `.gitignore`.
- Ignored all files by default.
- Re-allowed ignore policy files, agent TOML definitions, the README, and Markdown files under `docs`.

## Reasoning

This repository is an agent-definition catalog. The ignore policy should keep unrelated generated files, local caches, and accidental workspace artifacts out of version control while preserving the files needed to describe and maintain the agent definitions.

## Validation

- Reviewed `.gitignore` patterns to ensure no path pattern begins with a dot.
- No Python or Rust source files were changed, so Pyright and `cargo check` were not applicable.
