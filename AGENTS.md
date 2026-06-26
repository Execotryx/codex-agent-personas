# AGENTS.md

## Repository Purpose

This repository is a catalog of Codex custom-agent TOML definitions and their supporting documentation. Keep changes scoped to agent definitions, repository documentation, and maintenance files that directly support this catalog.

## File Scope

- Agent definitions live as root-level `*.toml` files.
- Repository documentation lives in `README.md`.
- Change logs live under `docs/` as dated Markdown files.
- Keep `.gitignore` allowlist-style: ignore unrelated files by default and allow only files needed for this agent catalog.
- When editing `.gitignore`, do not add patterns whose path starts with a dot. Use filename or extension patterns where needed.

## Documentation Rules

- Do not include real local machine paths, usernames, home-directory paths, or absolute workspace paths in README or docs.
- Prefer generic placement language for Codex configuration or agent locations.
- When adding, removing, renaming, or materially changing an agent definition, update `README.md`.
- Preserve migration metadata in `developer_instructions` unless the task explicitly changes the migration contract.
- Do not treat preserved Copilot source tools as an enforced Codex allowlist; document them as behavioral intent only.

## Validation

- After changing Python files, run Pyright if available. If Pyright is not available, try to add it with `uv add pyright`.
- After changing Rust files, run `cargo check` and fix any reported errors.
- For documentation-only changes, run a targeted `rg` scan for placeholders, real paths, or accidental local details relevant to the edit.
- For TOML agent-definition changes, verify each changed file still defines `name`, `description`, and `developer_instructions`.

## Change Logs

For every task that changes files, add a Markdown change log under `docs/`. The file name must include the creation date so logs are not overwritten. Each log should state:

- The task.
- The changes applied.
- The reasoning for those changes.
- The validation performed, including when Pyright or `cargo check` is not applicable.
