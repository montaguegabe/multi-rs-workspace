# multi-rs-workspace

Workspace for the Rust + Tauri remake of **multi**. Do **not** push to or modify the old public/private `multi`, `multi-desktop`, `multi-workspace`, or `multi-react` remotes from here.

## Gabe-stated target (2026-10-22)

- Implement **multi in Rust**.
- Replace the **Electron** desktop with **Tauri**.
- Use a **new workspace** and **new repos** (this tree). Do not reuse the existing multi repos as the remake destination.
- Use the **old multi** trees as **reference only**: the public `multi` workspace checkout (`multi-cli`, `multi-desktop`, `multi-react`); its location varies per machine.
- Work on **CTO’s computer (the box)** — not Gabe’s Mac for long-running Fable.
- Since 2026-11-01 the `multi` command on Gabe’s Mac is a shim that runs `cargo run --release` against this checkout’s `multi-rs` crate, so `main` here must always build and pass `cargo test`.
- Prefer Fable coding judgment for crate/layout details Gabe did not specify. Do not invent product scope beyond replacing multi’s workspace tooling + desktop with Rust + Tauri.

Agentic dispatch/coordination: machine-wide `~/AGENTS.md`.

## Layout

| Path | Repo | Purpose |
| --- | --- | --- |
| `multi-rs/` | montaguegabe/multi-rs | Rust multi (CLI/core) |
| `multi-rs-desktop/` | montaguegabe/multi-rs-desktop | Tauri desktop |

Reference (read-only): the original `multi` workspace checkout on the current machine.

## Status (2026-10-31)

- **Published and public (2026-11-10).** All repos here are public. The CLI repo ships to PyPI as `multi-workspace` via `.github/workflows/release.yml` (maturin `bin` wheels for macOS/Linux/Windows + sdist): every push to `main` publishes the next patch version, tags it and creates a GitHub release; raising `version` in the root `Cargo.toml` makes the next release that minor/major. 4.0.0 is the first Rust release; 3.x was Python. Publishing uses PyPI trusted publishing for this repo and workflow, or a `PYPI_API_TOKEN` secret when present. The old Python repo's release workflow was removed and its README points here.
- `multi-rs`: CLI/core implemented; `cargo test` passes on macOS and Linux.
- `multi-rs-desktop`: Tauri 2 + React app implemented over `multi-core`; builds and runs on macOS. Not yet done: release signing/notarization, updater feed, Windows/Linux verification.
- Ported (2026-11-01): `multi skills install [--dev]` from the Python CLI. `--dev` runs the `multi-skills` repo's `scripts/install-dev.sh` (from the BoilerSync `skills` template) to symlink the checkout into `~/.agents/skills` and `~/.claude/skills`; without it, `npx skills add` copies the published skills.
- 2026-11-01: `multi sync codex` (root `AGENTS.override.md` for Codex) and `multi sync skills` (root `.agents/skills` links) are implemented here with parity to the Python CLI. Both exist because Codex reads one instruction file per directory from the git root down to cwd and searches skills upward only, while Claude Code already discovers nested `CLAUDE.md` and `.claude/skills`; re-check both tools' discovery rules when touching them.

## Conventions

- Workspace git hooks live in `.githooks` (gitleaks on commit and push); `multi hooks status` should report every repo installed.

- Never check in secrets or Gabe personal absolute paths in published docs (local AGENTS may name box paths for agents).
- Never bind `0.0.0.0` / public listeners for local tooling.
- Commit and push each affected sub-repo, then this workspace root.
