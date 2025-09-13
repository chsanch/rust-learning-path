# Project: grep-lite

 - Goals:
  - Practice basic CLI in Rust (args, I/O, errors).
  - Reinforce ownership/borrowing with file reads and strings.

- Code: `${RUST_LEARN_REPO}/apps/grep-lite` (or repo-relative: `apps/grep-lite`)

 - Commands:
  - `cargo run --manifest-path apps/grep-lite/Cargo.toml -- "TODO" README.md`
  - `echo "hello\nworld" | cargo run --manifest-path apps/grep-lite/Cargo.toml -- -n -i "HELLO"`

 - Tasks (MVP):
  - [ ] Support `-n` (line number) and `-i` (ignore case).
  - [ ] Friendly error handling.
  - [ ] Basic tests (simple file and stdin).

 - Extensions (later):
  - [ ] Recursive `-r` via `walkdir`.
  - [ ] Extension filters `--ext rs,md`.
  - [ ] Optional regex `--regex` using the `regex` crate.

 - Learnings and notes:
  - 
