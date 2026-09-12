# Rust Learning Progress

Following the [Rust Fundamentals](rust-fundamentals/README.md) course (week 2 of the Pragmatic AI Labs Rust Bootcamp).

## Log

### 2026-09-10 — Lesson 1: Introduction to Rust
- **Architecture of a Cargo project**: `Cargo.toml` (manifest/recipe), `Cargo.lock` (locked dependency versions), `src/main.rs` (entry point), `target/` (compiled output, gitignored — regenerated, never committed).
- **Crates, packages, modules**: a *crate* is the compiler's unit of compilation — either a *binary crate* (`main.rs`, runnable) or a *library crate* (`lib.rs`, importable only). A *package* (one `Cargo.toml`) can produce one library crate + multiple binary crates. *Modules* organize code within a single crate. External library crates come from [crates.io](https://crates.io).
- **Hands-on**: created a practice project at [hello-crate](hello-crate) with `cargo new hello-crate`, inspected the generated `Cargo.toml` / `src/main.rs`, then ran `cargo run` and confirmed `target/` appears only after building.
- Reference example in the course repo: [examples/1-components](rust-fundamentals/examples/1-components).
- **`cargo new` vs `cargo init`**: `new` creates the project folder for you (nothing exists yet); `init` scaffolds into a folder that already exists (e.g. a freshly cloned empty GitHub repo) and takes the current folder's name instead of a name argument. Rule of thumb: no `Cargo.toml` in the folder → `new`/`init`; `Cargo.toml` already there (someone else's cloned project) → just `cargo build`/`cargo run`, no init needed.
- **`cargo check` vs `cargo build` vs `cargo run`**: each is a superset of the last — `check` type-checks only (fastest, no binary), `build` also generates the binary in `target/`, `run` also executes it. They're not a manual 3-step pipeline; `cargo run` does all of it in one command. `cargo check` (or an editor doing it continuously) is what you reach for when you just want fast error feedback.
- **Tooling installed for live error-checking**: `rustup component add rust-analyzer` (the language-server binary) + the `rust-lang.rust-analyzer` VS Code extension, so errors show up inline while typing instead of needing a manual `cargo check` in the terminal.
- **The story of `target/`**: it's a cache/snapshot, not source — `debug/` holds the compiled binary plus fingerprints/incremental data so the *next* build only recompiles what changed; `flycheck0/` is rust-analyzer's own private background `cargo check` output. Nothing in it is precious (`cargo clean` / delete it any time, it regenerates from source), which is why it's gitignored. Good practice is checking/building at natural development checkpoints (after each meaningful change), not on a time schedule — cheap because of that caching.
- **Where Rust sits between Java and C**: Cargo's tooling gives Java-like developer ergonomics (built-in dependency management, one-command build/test/run) but compiles to native machine code like C (no VM/JIT). The deeper "bridge" isn't tooling though — it's the borrow checker (upcoming in Lesson 3, [examples/14-borrowing](rust-fundamentals/examples/14-borrowing)), which gives Java-style memory safety enforced entirely at compile time, with no runtime garbage collector like Java needs and no manual `free()` like C requires.

## Up Next
- Variable assignment and immutability — [examples/2-variables](rust-fundamentals/examples/2-variables)
- Shadowing — [examples/4-shadowing](rust-fundamentals/examples/4-shadowing)
