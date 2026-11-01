# multi-rs-workspace

Private remake workspace for **multi** in Rust + Tauri. Do **not** push to or modify the old public/private `multi`, `multi-desktop`, `multi-workspace`, or `multi-react` remotes from here.

## Gabe-stated target (2026-10-22)

- Implement **multi in Rust**.
- Replace the **Electron** desktop with **Tauri**.
- Use a **new workspace** and **new private repos** (this tree). Do not reuse the existing multi repos as the remake destination.
- Use the **old multi** trees as **reference only**: the public `multi` workspace checkout (`multi-cli`, `multi-desktop`, `multi-react`); its location varies per machine.
- Work on **CTO’s computer (the box)** — not Gabe’s Mac for long-running Fable.
- Prefer Fable coding judgment for crate/layout details Gabe did not specify. Do not invent product scope beyond replacing multi’s workspace tooling + desktop with Rust + Tauri.

Agentic dispatch/coordination: machine-wide `~/AGENTS.md`.

## Layout

| Path | Repo | Purpose |
| --- | --- | --- |
| `multi-rs/` | montaguegabe/multi-rs (private) | Rust multi (CLI/core) |
| `multi-rs-desktop/` | montaguegabe/multi-rs-desktop (private) | Tauri desktop |

Reference (read-only): the original `multi` workspace checkout on the current machine.

## Status (2026-10-31)

- `multi-rs`: CLI/core implemented; `cargo test` passes on macOS and Linux.
- `multi-rs-desktop`: Tauri 2 + React app implemented over `multi-core`; builds and runs on macOS. Not yet done: release signing/notarization, updater feed, Windows/Linux verification.
- Ported (2026-11-01): `multi skills install [--dev]` from the Python CLI. `--dev` runs the `multi-skills` repo's `scripts/install-dev.sh` (from the BoilerSync `skills` template) to symlink the checkout into `~/.agents/skills` and `~/.claude/skills`; without it, `npx skills add` copies the published skills.
- Parity gap (2026-11-01): the Python CLI gained `multi sync skills`, which links each sub-repo's `.agents/skills/<name>` into the root `.agents/skills` so Codex discovers them (Codex searches upward only; Claude Code already finds nested `.claude/skills`, so those are not linked). Port it to `multi-core`'s sync, and re-check both tools' discovery rules when doing so.

## Conventions

- Workspace git hooks live in `.githooks` (gitleaks on commit and push); `multi hooks status` should report every repo installed.

- Never check in secrets or Gabe personal absolute paths in published docs (local AGENTS may name box paths for agents).
- Never bind `0.0.0.0` / public listeners for local tooling.
- Commit and push each affected private sub-repo, then this workspace root.
