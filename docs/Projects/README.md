# Projects Notes

This folder contains per-project notes (objectives, tasks, and commands).

Conventions:
- Use repo-relative paths in commands.
- On `main`, prefer per-crate commands with `--manifest-path` (no workspace on `main`).
- On lesson branches (solutions), workspace-wide commands are fine.

Example (grep-lite):
- `cargo run --manifest-path apps/grep-lite/Cargo.toml -- "pattern" README.md`
