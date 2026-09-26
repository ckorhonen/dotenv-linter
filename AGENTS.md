# dotenv-linter repository guide

This Rust workspace separates `dotenv-analyzer`, `dotenv-cli`, `dotenv-core`, `dotenv-finder`, and `dotenv-schema`. Follow the existing analyzer/rule and fixture patterns; don't assume an old contribution example's `src/checks` path is the current root layout. Use synthetic environment values and never inspect or print a user's real `.env` for a test.

Use a stable Rust toolchain supporting edition 2024, with rustfmt and Clippy. From the root, CI checks `cargo check --all-targets --tests --examples --benches`, `cargo fmt --all --check`, `cargo clippy --all-features --tests --examples --benches -- -D warnings`, and `cargo test --all-features --no-fail-fast`. Run the affected crate/test first for a narrow change; there is no independent typecheck step beyond Rust compilation. Coverage uses additional tooling and is separate from normal tests.

Build the relevant binary with Cargo and use temporary fixtures to exercise lint/fix behavior. Fix mode rewrites environment files, so don't use production configuration as a smoke test. Preserve diagnostics, ordering, exit status, and no-value-disclosure behavior; a formatter or build pass alone does not verify a new lint rule.

## Completing work

Carry the authorized change through the relevant checks and repair failures it causes. Make routine, reversible implementation choices using existing patterns; ask only when missing information, a material product decision, or an authorization boundary prevents the next step. Existing authorization remains valid within its scope. If blocked, name the exact action and missing prerequisite, retain concise evidence, and continue independent work.

Choose verification proportional to the change. For instructions or prose, inspect changed paths, links, and local instruction precedence and run `git diff --check -- <changed-paths>`; don't install dependencies or run the application solely for a prose edit. For behavior changes, exercise the affected behavior and applicable checks below, then broaden only for failures or unresolved risk. Report files changed, checks actually run and their results, commands only inspected, and remaining limitations. A build or source inspection alone does not prove runtime behavior. Continue through already-authorized follow-through; stop at explicit review checkpoints or boundaries requiring new authorization.
