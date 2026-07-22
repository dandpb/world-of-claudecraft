# Codex source router

`src/CLAUDE.md` owns cross-source architecture. Read it in full, then read the nearest
directory-local `CLAUDE.md` before inspecting or changing that area. This file only routes
Codex work and reviewer selection.

## Where to look

| Change | Canonical guide |
|---|---|
| Simulation systems or content | `sim/CLAUDE.md`, then the nearest nested guide |
| Rendering or character rigs | `render/CLAUDE.md`, optionally `render/characters/CLAUDE.md` |
| HUD, i18n, or CSS | `ui/CLAUDE.md`, `ui/hud/CLAUDE.md`, `styles/CLAUDE.md` |
| Input, camera, audio, native controls | `game/CLAUDE.md` |
| Online client or wire mirror | `net/CLAUDE.md` |
| `IWorld` facets | `world_api/CLAUDE.md` |
| Admin, guide, or editor SPA | The matching directory's `CLAUDE.md` |

## Codex routing

- Simulation edits require `woc_sim_architecture`; add `woc_cross_platform` when a host,
  command, event, matcher, or `IWorld` surface can drift.
- UI, render, styles, accessibility, i18n, or graphics-setting edits require `woc_frontend`.
- Behavior tests or parity pins require `woc_test_coverage`.
- Security-sensitive admin or native-shell changes also require `woc_security`.

## Checks

- Use the smallest paired Vitest file while iterating.
- Run `tests/architecture.test.ts` for sim or presentation-seam changes.
- Run `tests/world_api_parity.test.ts` and command pins for an `IWorld` or wire change.
- Finish through the root `$woc-qa` workflow; the coordinator owns shared gate commands.
