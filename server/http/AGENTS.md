# Codex REST pipeline router

Read root `CLAUDE.md`, `server/CLAUDE.md`, and this directory's `CLAUDE.md` before work.
The local `CLAUDE.md` owns the full pipeline contract; this file routes implementation,
tests, and reviewers.

## Where to look

| Task | Location |
|---|---|
| Add an endpoint | `npm run new:endpoint`, domain `routes`, `registry.ts` |
| Change dispatch behavior | `dispatch.ts`, `compose.ts`, paired `tests/server/http/` suite |
| Change routing | `router.ts`, `path_pattern.ts`, surface inventory and parity tests |
| Change request guards | `middleware/`, same-named middleware test |
| Change validation or errors | `schema.ts`, `errors.ts`, append-only `error_codes.ts` |
| Add metrics | Existing registry, signals, and periodic collector seams |

## Codex routing

- Route, middleware, auth, ownership, CORS, upload, or error changes require
  `woc_security`.
- DB-backed metrics or endpoint queries require `woc_database_performance`; persistence
  shape changes also require `woc_persistence`.
- Any behavior change requires `woc_test_coverage` and the characterization spine.

## Required checks

- Run the same-named unit test for the changed pipeline module.
- For route additions or removals, run surface inventory, completeness, and parity tests.
- Follow the dual-edit rule in the local `CLAUDE.md` for routes served by both dispatch
  arms.
- Finish through the parent `$woc-qa` workflow.
