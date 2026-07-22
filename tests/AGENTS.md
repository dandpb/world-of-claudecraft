# Codex test router

Read root `CLAUDE.md` and `tests/CLAUDE.md` before test work. Read
`parity/CLAUDE.md` before touching golden traces. The canonical guides own test idioms;
this file routes coverage and execution.

## Where to look

| Test shape | Location |
|---|---|
| Paired unit or behavior test | Flat `tests/<module>.test.ts` |
| REST pipeline or RouteDef | `tests/server/` and shared `tests/server/helpers/` |
| Svelte admin component | `tests/admin/` with its local setup import |
| Real-browser behavior | `tests/browser/*.browser.test.ts` |
| Deterministic sim drift | `tests/parity/` |
| Shared lightweight DOM | `tests/helpers/fake_dom.ts` |

## Codex routing

- Added or modified tests, acceptance claims, and regression fixes require
  `woc_test_coverage`.
- Sim fixtures or parity traces also require `woc_sim_architecture` when production sim
  code changes.
- Server, frontend, persistence, and wire reviewers inspect the test evidence for their
  changed domains; they do not replace coordinator-owned commands.

## Checks

- Run the execution idiom `tests/CLAUDE.md` documents for the touched suite (focused
  single-file runs, the browser suite, parity regeneration).
- Finish through root `$woc-qa` and report exact commands and outcomes.
