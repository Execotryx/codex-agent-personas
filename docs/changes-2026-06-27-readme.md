# Change Log - 2026-06-27 - Repository README

## Task

Traverse the repository and create a detailed README without inventing behavior, using Codex documentation as the basis for Codex-specific claims.

## Changes Applied

- Added `README.md` describing the repository as a catalog of Codex custom-agent TOML files.
- Documented the official Codex custom-agent placement and required fields using the current Codex manual.
- Added an agent catalog table covering every TOML file in the repository.
- Grouped agents by observed purpose: migration/porting, planning/debugging/refactoring, performance, and ML/hardware workflows.
- Documented the declared collaboration graph and sandbox defaults from the agent metadata.
- Added maintenance and validation guidance for future documentation or agent-definition edits.

## Reasoning

The repository had no README, docs folder, or change log. A README is needed so users can understand what each custom-agent file is for, where Codex expects such files to live, which fields are required, and which local agent relationships are declared. The README avoids claiming runtime behavior beyond the official Codex manual and the metadata present in the TOML files.

## Validation

- Consulted the current official Codex manual via the `openai-docs` skill.
- Inspected all repository TOML files and extracted their declared metadata.
- No Python or Rust source files were changed, so Pyright and `cargo check` were not applicable.
