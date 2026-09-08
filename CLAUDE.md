# Sanctuary — Project Guide for Claude

Solo game project by Alex. Zombie/infection **town-survival sim** built in **Unreal Engine 5.8 (Blueprints first)**, with Blender and Claude Code. Target: playable PC vertical slice.

## Where things are
- **Project root (git root):** this folder — `Documents/Unreal Projects/Sanctuary/Sanctuary/` (the `.uproject` is here).
- **Repo:** private, `git@github.com:alexfferrara-coder/Sanctuary.git` (SSH). GitHub account `alexfferrara-coder`.
- **Roadmap (the 9 phases):** [`docs/ROADMAP.md`](docs/ROADMAP.md) — Gantt + per-phase checklists. **Read it every session; keep it honest** (tick boxes as work lands, move the `👉 CURRENT` marker).
- **Content layout:** `Content/ThirdPerson/Blueprints/` (character, game mode, controller), `Content/Input/` (`IMC_Default`, `IMC_MouseLook`, `Actions/IA_*`), `Content/Characters/Mannequins/` (Quinn placeholder character).

## Working conventions
- **Track progress in two places:** `docs/ROADMAP.md` checkboxes, and **GitHub Issues** (one per system, labeled `phase-2`…`phase-9`). Close the matching issue when a system ships (`Closes #N` in the commit).
- **Alex is new to Unreal** — for any step done by hand in the editor, give **click-by-click** instructions (exact panel/menu/pin/checkbox). Do as much as possible via the Unreal MCP so Alex does less. Gotcha: Blueprint node values (checkboxes) are only clickable when **zoomed in** — the graph disables them at low zoom.
- **Commit/push:** commit and push only when asked. Auto-mode may block `git push` from Claude — if so, hand Alex the `!`-prefixed command to run.
- **Documentation principle:** CLAUDE.md and memory describe only what *exists now*. Future/planned work goes in `docs/ROADMAP.md`, not in active sections here.

## Unreal MCP (live editor control)
- The `unreal` MCP server (`ue_*` tools) drives the editor **only while it's open**. If tools report no editor, ask Alex to open `Sanctuary.uproject`.
- Remote execution is enabled and pinned to all interfaces via `Config/DefaultEngine.ini` → `RemoteExecutionMulticastBindAddress=0.0.0.0` (required — UE 5.8 defaults to loopback-only, which the MCP bridge can't discover). Don't remove that line.
- Blueprint **event-graph node wiring cannot be scripted** via the MCP Python bridge (no node-spawning API). Do component/asset/variable-type-limited work via MCP; hand off graph wiring as click-by-click steps.
- To test gameplay input, use a **possessed Play** (`LevelEditorSubsystem.editor_request_begin_play()`), not Simulate — Simulate doesn't possess the character so input won't route.

## Current status
- **Phase 1:** complete (pipeline, MCP, private repo + LFS).
- **Phase 2 (current):** switchable first/third-person camera ✅, Enhanced Input + gamepad bindings ✅. Next: interact system. See `docs/ROADMAP.md` for the rest.

## Git commit / PR attribution
- End commit messages with:
  `Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>`
- Assets are binary; **Git LFS** tracks `.uasset`/`.umap` (see `.gitattributes`). Free-tier LFS is 1 GB — fine until real assets/Megascans arrive (Phase 8).
