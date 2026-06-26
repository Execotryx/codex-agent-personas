# Change Log - 2026-06-27 - README Path Scrub

## Task

Review the README and ensure it contains no real local paths.

## Changes Applied

- Removed the machine-specific Windows directory from the README introduction.
- Reworded the Codex documentation basis to describe personal and project-scoped custom-agent placement without spelling out home-directory paths.

## Reasoning

The README should be portable and safe to share. Local absolute paths and user-home examples can expose environment details or imply a placement that is specific to one machine.

## Validation

- Searched the README for Windows drive paths, user-home paths, the local username, and explicit Codex directory paths.
- No Python or Rust source files were changed, so Pyright and `cargo check` were not applicable.
