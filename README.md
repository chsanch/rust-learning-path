# Rust Learning Workspace

This repository is a Rust workspace to learn by building projects, with a tutorial and notes under `docs/`.

Repository: git@github.com:chsanch/rust-learning-path.git

- Code: `apps/` contains project binaries (e.g., `apps/grep-lite`).
- Notes: `docs/` is a versioned directory; you can open this repo as an Obsidian Vault.

Path conventions (optional):
- `RUST_LEARN_REPO` → local path to this repo.
- `RUST_NOTES_DIR` → only if you externalize notes (see AGENTS.md).

## Quick use

- Format: `cargo fmt`
- Lints: `cargo clippy -- -D warnings`
- Tests: `cargo test`
- Run grep-lite:
  - `cargo run -p grep-lite -- "foo" ./README.md`
  - `echo "hello\nworld" | cargo run -p grep-lite -- -n -i "HELLO"`

## Structure

- `Cargo.toml` (workspace)
- `apps/` (projects)
- `docs/` (versioned notes)

## Next steps

- Add tests to `grep-lite` and improve error handling.
- Extend with recursive search and filters.

## Branch model (learn and share)

- `main`: tutorial only, no solutions (checklists unchecked). Ideal for starting from scratch.
- `lesson/<nn>-<slug>`: solution branches per lesson, e.g., `lesson/01-grep-lite`.
- Tags: after finishing a lesson, create `lesson-<nn>` on that branch.

Per-lesson flow:
- On `main`, add/update the lesson in `docs/Tutorial/` and project TODOs.
- Create a branch: `git switch -c lesson/<nn>-<slug>`.
- Implement the solution, mark TODOs, add tests, and tag `lesson-<nn>`.
- Don’t merge solutions into `main`; an optional `solutions` branch can aggregate them.

## Remote setup

If this is your first time setting up the remote:

- `git remote add origin git@github.com:chsanch/rust-learning-path.git`
- Push the tutorial baseline: `git push -u origin main`
- Push lesson branches/tags as needed:
  - `git push -u origin lesson/00-prerequisites`
  - `git push -u origin lesson/01-grep-lite`
  - `git push origin --tags`
