# Codex tooling router

Read root `CLAUDE.md` and `scripts/CLAUDE.md` before tool changes. Read the nearest
local `CLAUDE.md` under `assets/`, `asset_pipeline/`, `profiler/`, or `sfx_studio/`.
The canonical guides own tool behavior; this file routes safe execution and review.

## Where to look

| Tool class | Primary seam |
|---|---|
| CI-equivalent gate | `gate.mjs` and `.github/workflows/ci.yml` |
| Browser or screenshot automation | `browser_path.mjs`, shared entry helpers |
| Multiplayer integration | Existing client and snapshot merge helpers |
| Build generation | The owning `build_*.mjs` plus its freshness test |
| Asset, profiler, or SFX tooling | The matching subdirectory and local `CLAUDE.md` |
| Pure reusable logic | `lib/` or the owning subsystem with a paired test and declaration |

## Codex routing

- Releases, dependencies, install behavior, AI instructions, or suspicious executable
  content require `woc_release_malware`.
- Production ops, credentials, uploads, admin utilities, or external process execution
  require `woc_security`.
- SQL or database utility changes require `woc_database_performance` and, when persisted
  shape or compatibility is involved, `woc_persistence`.
- Changed script logic or gates require `woc_test_coverage`.

## Checks

- Run the paired unit or characterization test for the changed script.
- Exercise a CLI through its real entry point when behavior changes.
- Keep `gate.mjs` aligned with CI and finish through root `$woc-qa`.
