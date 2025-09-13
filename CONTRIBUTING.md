# Contributing

Thank you for your interest in improving this Rust learning workspace.

Repository: git@github.com:chsanch/rust-learning-path.git

## Language and style
- Primary language: English (tutorial, docs, code messages).
- Be concise and practical; prefer runnable examples and short explanations.
- Use monospace for commands and paths.

## Branch model
- `main`: tutorial only, no solutions (unchecked checklists). Do not add final code here.
- `lesson/<nn>-<slug>`: per-lesson solution branches, e.g. `lesson/01-grep-lite`.
- Optional `solutions`: aggregate branch for all solutions; never merge into `main`.

Per-lesson flow:
1) On `main`, add/update the lesson under `docs/Tutorial/` and the project note under `docs/Projects/`.
2) Create a branch: `git switch -c lesson/<nn>-<slug>`.
3) Implement code under `apps/`/`libs/`, mark tasks in notes, add tests.
4) Commit and tag: `git add -A && git commit -m "lesson(<nn>): <summary>" && git tag -a lesson-<nn> -m "Lesson <nn>: <title>"`.

## Commit history policy (single-commit per lesson)
- Keep `main` clean and readable, ideally one commit per lesson:
  - Example main history: `starting the project`, `add lesson 0: prerequisites`, `add lesson 1: grep-lite`.
  - Do not commit solutions to `main`; only tutorial/doc updates with unchecked TODOs.
- Aim for a single commit on each `lesson/<nn>-<slug>` branch:
  - Prepare all work locally and squash before tagging.
  - Options to squash:
    - Soft reset: `git reset --soft <base> && git commit -m "adding lesson <nn>"`
    - Orphan root: `git switch --orphan lesson/<nn>-<slug> && git add -A && git commit -m "adding lesson <nn>"`
  - Retag if needed: `git tag -f -a lesson-<nn> -m "Lesson <nn>: <title>"`
- Rationale: avoid noise in `main` and keep lesson branches tidy; contributors can still use any workflow in their own forks.

## Quality
- Run `cargo fmt`, `cargo clippy -- -D warnings`, and `cargo test` before submitting changes.
- Favor small, focused commits with descriptive messages.

## Docs
- Keep `docs/` as the source of truth for the tutorial. Update links when renaming files.
- Prefer repo-relative paths (e.g., `apps/...`) or `${RUST_LEARN_REPO}` when needed.

## PRs
- PRs to `main` must not include solution `.rs` files under `apps/` or `libs/`.
- Include rationale for changes and, when applicable, before/after examples.
