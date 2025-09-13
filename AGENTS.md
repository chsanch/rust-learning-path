# AGENTS.md — Workspace guide and plan

Purpose: This repository is a Rust learning workspace organized around practical, project-based lessons. Documentation lives in the versioned `docs/` folder.

Repository URL: `git@github.com:chsanch/rust-learning-path.git`

- Code root: `${RUST_LEARN_REPO}` (path is user-defined)
- Notes: `docs/` inside this repo (can be opened as an Obsidian vault)

## Goals
- Learn Rust by building incremental projects (CLI, async, web, DB, WASM).
- Keep living documentation of decisions, takeaways, and tasks per project.
- Maintain quality from day one: formatting, lints, and tests.

## Structure
- On `main` (tutorial only):
  - `docs/` versioned documentation for the tutorial (index + lessons)
  - `README.md`, `AGENTS.md`, `CONTRIBUTING.md`
- On lesson branches (solutions):
  - `Cargo.toml` (workspace, resolver=2)
  - `apps/` binaries per project (e.g., `apps/grep-lite`)
  - `libs/` reusable libraries (as needed)
  - `examples/` small topic-focused exercises
  - `justfile` common tasks

## Workflow
1) New project
- Create a crate in `apps/<name>` or `libs/<name>` as appropriate.
- Create a note in `docs/Projects/<name>.md` using `docs/Templates/Project.md`.
- Define goals, checklist, and runnable commands.

2) Development
- Cycle: code → `cargo fmt` → `cargo clippy -- -D warnings` → `cargo test` → update the note with decisions and open questions.
- For binaries use `anyhow`; for libraries prefer `thiserror` + `Result<T, E>`.

3) Weekly review
- 1 main project + 1–2 short reinforcement exercises.
- Capture takeaways and next steps in the project note.

## Conventions
- Edition 2021. Avoid `unwrap()` except in tests or well-justified cases.
- Keep modules simple; separate I/O from core logic when possible.
- Tests: unit tests next to code; integration tests under `tests/`.
- Lints: deny warnings; enable Clippy (prefer `warn`/`pedantic`) and fix before merging.
- Atomic, descriptive commits (Conventional Commits encouraged).

## Tooling (on lesson branches)
- Formatting: `cargo fmt`
- Lints: `cargo clippy -- -D warnings`
- Tests: `cargo test`
- Justfile: `just fmt`, `just clippy`, `just test`, `just run-grep <pattern> <file>`

## Notes and Obsidian
- Current state: `docs/` is a versioned directory in the repo.
- Recommended: open this repo as an Obsidian Vault and edit notes under `docs/`.
- CI/agents: writing to `docs/` requires no special permissions (it’s inside the repo).

## Portable path conventions
- Optional environment variables:
  - `RUST_LEARN_REPO` → repo root path (e.g., `~/Projects/rust`).
- In docs, prefer repo-relative paths (`apps/...`) or `${RUST_LEARN_REPO}` when needed.

## If you ever externalize notes
- Symlink or submodule are options, but both have trade-offs (symlinks aren’t portable; submodules add complexity). Default: keep `docs/` versioned in this repo.

## Default policy
- Keep `docs/` as a versioned directory and use this repo as the primary Vault for sharing code and notes together.

## Initial plan (milestones)
- Week 1 – Fundamentals + CLI: `apps/grep-lite`
  - MVP: `-n`, `-i`, file or stdin.
  - Extensions: recursive `-r` (walkdir), extension filters, `--regex`.
- Week 2 – Structs/errors: `apps/todo-cli` (serde, thiserror/anyhow)
- Week 3 – Generics/traits/iterators: `libs/csv-utils` + `apps/csv-summarizer`
- Week 4 – Quality/tests: more coverage and property-based with `proptest`
- Week 5 – Async: `apps/httpie` (tokio/reqwest)
- Week 6 – Web: `apps/url-shortener` (axum/actix)
- Week 7 – DB: persistence for `url-shortener` (sqlx/SQLite or Postgres)
- Week 8 – WASM/Node interop: `apps/md-preview-wasm` or `napi-rs`

## How to run (on a lesson branch)
- `cargo run -p grep-lite -- "foo" ./README.md`
- `echo "hello\nworld" | cargo run -p grep-lite -- -n -i "HELLO"`
- `just` to list available tasks.

## Remote and publishing
- Set remote if missing: `git remote add origin git@github.com:chsanch/rust-learning-path.git`
- Push tutorial baseline: `git push -u origin main`
- Push lesson branches and tags:
  - `git push -u origin lesson/00-prerequisites`
  - `git push -u origin lesson/01-grep-lite`
  - `git push origin --tags`

## Definition of Done (DoD)
- Builds clean with Clippy and passes tests.
- Project note updated with goals, decisions, and open items.
- Reproducible run instructions in the note and/or README.

## Tutor/Learner mode
- Agent role: act as a tutor. Provide concrete steps with commands and a short explanation. Ask the learner to run and share results.
- Living docs: for each lesson, create/update `docs/Tutorial/` and the project note in `docs/Projects/<app>.md`.
- Lesson structure:
  - Index: `docs/Tutorial/00-index.md`.
  - One note per lesson: `docs/Tutorial/<nn>-<topic>.md` with:
    - A "Create your branch" preamble (e.g., `git switch -c my/lesson-<nn>`) so learners isolate their work from `main`.
    - Objectives, prerequisites, steps (command + purpose), challenges, key concepts, and a Q&A log.
  - Link to relevant code and reproducible `cargo` commands.
- Interaction cadence:
  - Share a brief preamble before automated actions (what and why).
  - Prefer the learner to execute commands; the agent only runs when asked/approved.
- Agent tools:
  - Maintain an up-to-date plan with `update_plan`.
  - Use `apply_patch` for repo changes.
  - Avoid destructive actions; don’t add unnecessary tooling.
- Language and style:
  - Clear, concise English. Commands in monospace.
  - 1–2 line explanations per command, focused on purpose.
  - Record Q&A and decisions in the corresponding notes.

## Lesson 0 — Prerequisites and environment
- Ensure the learner has Git, Rust (rustup + stable toolchain), `clippy`, and `rustfmt`. Editor with `rust-analyzer`. Optional: `just` and `cargo-watch`.
- Document these steps in `docs/Tutorial/00-prerequisites.md` and link from `docs/Tutorial/00-index.md`.

## Per-lesson versioning (commits/tags)
- After each lesson:
  - `git add .`
  - `git commit -m "lesson(<nn>): <summary>"`
  - `git tag -a lesson-<nn> -m "Lesson <nn>: <title>"`
- Record tag/hash in the lesson note and the index.
- Policy: the agent does not run `git commit/tag` without explicit approval; it proposes commands.

## Git strategy (main without solutions)
- Branch roles:
  - `main`: tutorial documentation and templates only. Checklists remain unchecked. No solutions or final code.
  - `lesson/<nn>-<slug>`: per-lesson branches with full implementation and checked tasks. E.g., `lesson/01-grep-lite`.
  - Optional `solutions`: aggregate branch for all solutions (never merged into `main`).
- Per-lesson flow:
  1) On `main`, add/update the lesson in `docs/Tutorial/` and the project note in `docs/Projects/` (no solutions). Commit on `main`.
  2) Create branch: `git switch -c lesson/<nn>-<slug>`.
  3) Implement code in `apps/`/`libs/`, mark tasks in notes, add tests.
  4) `git add -A && git commit -m "lesson(<nn>): <summary>" && git tag -a lesson-<nn> -m "Lesson <nn>: <title>"`.
  5) (Optional) Integrate into `solutions`; never merge solutions into `main`.
- Rules for `main`:
  - Don’t add solution `.rs` files under `apps/` or `libs/`. If a skeleton is needed, keep minimal placeholders or use templates under `docs/Templates/`.
  - PRs to `main` should only modify docs/templates/guides.

## Commit history policy (single-commit per lesson)
- Main timeline should stay clean and readable, ideally one commit per lesson:
  - Example: `starting the project`, `add lesson 0: prerequisites`, `add lesson 1: grep-lite`, ...
  - Main commits must not include solutions; only tutorial/docs updates and unchecked TODOs.
- Lesson branches should also aim for a single commit (clean history):
  - Prepare all changes locally, then create a single commit (squash beforehand).
  - Two ways to achieve this:
    - Soft reset squash: `git reset --soft <base> && git commit -m "adding lesson <nn>"`
    - Orphan root commit: `git switch --orphan lesson/<nn>-<slug> && git add -A && git commit -m "adding lesson <nn>"`
  - Retag after squashing: `git tag -f -a lesson-<nn> -m "Lesson <nn>: <title>"`
- Rationale: avoids noise in `main` history and keeps per-lesson branches tidy. Learners can still use their preferred workflow in their own forks/branches.
