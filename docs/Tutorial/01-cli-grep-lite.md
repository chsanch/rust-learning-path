# Lesson 1 — CLI: grep-lite

Before you start — Create your branch
- Command: `git switch -c my/lesson-01`
- Why: keeps your solution separate from `main` (tutorial-only).

Goal: build, run, and understand a basic CLI in Rust, reinforcing I/O, argument parsing, and strings.

Prerequisites:
- Have Rust installed (`rustup`, `cargo`). If not, see https://rustup.rs.

## Guided steps

1) Verify toolchain
- Command: `rustc --version && cargo --version && rustup show active-toolchain`
- Why: ensures Rust and Cargo are available and shows the active toolchain.

2) Create the lesson project
- Command: `mkdir -p apps && cargo new apps/grep-lite --bin`
- Why: scaffolds a binary crate named `grep-lite` under `apps/`.

3) Inspect the workspace
- Command: `ls -la && (tree -L 2 apps || find apps -maxdepth 2 -type d -print)`
- Why: confirm the structure and that `apps/grep-lite` exists.

4) Formatting and lints (good habit early)
- Command: `cargo fmt --manifest-path apps/grep-lite/Cargo.toml`
- Command: `cargo clippy --manifest-path apps/grep-lite/Cargo.toml -- -D warnings`
- Why: format and lint just this crate (no workspace on main).

5) Build the project
- Command: `cargo build --manifest-path apps/grep-lite/Cargo.toml`
- Why: builds only the `grep-lite` crate and fetches dependencies.

6) Run with a file
- Command: `cargo run --manifest-path apps/grep-lite/Cargo.toml -- "Rust" ./README.md`
- Why: searches for the word "Rust" in the repo README.

7) Run with stdin
- Command: `echo "hello\nworld" | cargo run --manifest-path apps/grep-lite/Cargo.toml -- -n -i "HELLO"`
- Why: demonstrates flags `-n` (line numbers) and `-i` (ignore case) reading from stdin.

8) Controlled error test
- Command: `cargo run -p grep-lite -- "x" ./does-not-exist.txt; echo $?`
- Why: observe exit code and message; later we’ll improve UX with `anyhow`/custom messages.

## Quick challenges
- Run against this file: `cargo run --manifest-path apps/grep-lite/Cargo.toml -- "grep-lite" apps/grep-lite/src/main.rs`
- Change the pattern and re-run tests with/without `-i` and `-n`.
- Write 2–3 observations in this section.

## Key concepts to notice
- `clap` for argument parsing.
- Reading from file vs. stdin and error handling.
- `&str` vs `String`; conversions and costs.

## Next steps (after this lesson)
- Add basic tests (small file and stdin).
- Improve error messages and exit codes.
- Extension: recursive `-r` using `walkdir`.

## Q&A log
- (Record your questions and answers here; we’ll keep this live.)
