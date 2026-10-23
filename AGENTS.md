# multi-rs-workspace

Private remake workspace for **multi** in Rust + Tauri. Do **not** push to or modify the old public/private `multi`, `multi-desktop`, `multi-workspace`, or `multi-react` remotes from here.

## Gabe-stated target (2026-10-22)

- Implement **multi in Rust**.
- Replace the **Electron** desktop with **Tauri**.
- Use a **new workspace** and **new private repos** (this tree). Do not reuse the existing multi repos as the remake destination.
- Use the **old multi** trees as **reference only** (on this machine: `../reference/multi`, `../reference/multi-desktop`, etc.).
- Work on **CTO’s computer (the box)** — not Gabe’s Mac for long-running Fable.
- Prefer Fable coding judgment for crate/layout details Gabe did not specify. Do not invent product scope beyond replacing multi’s workspace tooling + desktop with Rust + Tauri.

Agentic dispatch/coordination: machine-wide `~/AGENTS.md`.

## Layout

| Path | Repo | Purpose |
| --- | --- | --- |
| `multi-rs/` | montaguegabe/multi-rs (private) | Rust multi (CLI/core) |
| `multi-rs-desktop/` | montaguegabe/multi-rs-desktop (private) | Tauri desktop |

Reference (read-only): `/home/box/Projects/multi-rs/code/reference/`

## Conventions

- Never check in secrets or Gabe personal absolute paths in published docs (local AGENTS may name box paths for agents).
- Never bind `0.0.0.0` / public listeners for local tooling.
- Commit and push each affected private sub-repo, then this workspace root.
