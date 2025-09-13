# Lesson 0 — Prerequisites and environment

Goal: Set up your environment (Rust, editor, utilities, Git) and agree on per-lesson commit/tag practice.

## Checklist
- [ ] Git installed and available on PATH
- [ ] Rustup installed, stable toolchain set as default
- [ ] Clippy and rustfmt installed
- [ ] rustc/cargo/toolchain versions verified
- [ ] Editor with rust-analyzer ready
- [ ] Optional: just installed
- [ ] Optional: cargo-watch installed
- [ ] Repo cloned and in the correct directory
- [ ] Optional: open repo as an Obsidian Vault

## 1) Install Git
- macOS (Homebrew): `brew install git`
- Debian/Ubuntu: `sudo apt-get update && sudo apt-get install -y git`
- Arch: `sudo pacman -S git`
- Windows: install Git and optionally WSL2; alternative: Git for Windows.

## 2) Install Rust (rustup)
- Official installer: https://rustup.rs
- Set stable as default: `rustup update stable && rustup default stable`
- Useful components: `rustup component add clippy rustfmt`

Verify:
- `rustc --version && cargo --version && rustup show active-toolchain`
- `cargo clippy -V && rustfmt -V`

## 3) Recommended editor
- Zed (fast, native, great Rust support): see https://zed.dev/docs/languages/rust
- VS Code + `rust-analyzer` extension.
- Alternatives: JetBrains (Rust plugin), Neovim (rust-tools.nvim), etc.

## 4) Optional utilities
- `just` task runner: macOS `brew install just`; Linux `cargo install just`.
- `cargo-watch` for live rebuilds: `cargo install cargo-watch`.

## 5) Get this repo or create the workspace
- Clone: `git clone git@github.com:chsanch/rust-learning-path.git ${RUST_LEARN_REPO:-$HOME/Projects/rust} && cd ${RUST_LEARN_REPO:-$HOME/Projects/rust}`
- From scratch: create a folder and initialize as needed.

## 6) Notes (Obsidian recommended)
- Open this repository as an Obsidian Vault to edit `docs/` directly (versioned directory).
- Alternatives (if keeping notes outside the repo): see `AGENTS.md` (symlink or submodule under `docs/`).

## 7) Path conventions and per-lesson commits/tags
- Optional: define `RUST_LEARN_REPO` for documentation convenience:
  - `export RUST_LEARN_REPO="$HOME/Projects/rust"`
- After each lesson:
  - `git add .`
  - `git commit -m "lesson(00): environment ready"`
  - `git tag -a lesson-00 -m "Lesson 0: environment"`
- Repeat for each lesson: `lesson-01`, `lesson-02`, etc., and record tag/hash in the lesson note.

## 8) Next step
- Branches:
  - To follow the tutorial without solutions, work on `main`.
  - To implement a lesson, create a branch: `git switch -c lesson/<nn>-<slug>`.
  - When done, tag it: `git tag -a lesson-<nn> -m "Lesson <nn>"`.
- Continue with “Lesson 1 — CLI: grep-lite”.
