# Codex server router

Read the root `CLAUDE.md` and `server/CLAUDE.md` in full before server work. Read the
nearest nested `CLAUDE.md` for `http/`, `email/`, or `steam/`. Those files own all server
facts and invariants; this file owns Codex review routing.

## Where to look

| Change | Primary seam |
|---|---|
| HTTP or WS process wiring | `main.ts` |
| Authoritative world loop | `game.ts` plus shared `src/sim/` systems |
| REST route or middleware | `http/AGENTS.md` and `http/CLAUDE.md` |
| Persistence or schema | `db.ts` or the owning `*_db.ts` |
| Authentication or moderation | The owning pure core plus injected service shell |
| Email or Steam integration | The matching directory's `CLAUDE.md` |

## Codex routing

- All auth, moderation, admin, trust-boundary, upload, or secret changes require
  `woc_security`.
- DDL, persisted JSONB shape, save/load, leases, or compatibility require `woc_persistence`.
- SQL, database call sites, query cadence, indexes, pools, locks, timeouts, background DB
  work, or stored-data growth require `woc_database_performance` before decisions and on
  the finished diff.
- Wire, event, command, snapshot, matcher, or shared-sim changes require
  `woc_cross_platform`; simulation changes also require `woc_sim_architecture`.
- New or changed behavioral coverage requires `woc_test_coverage`.

## Checks

- Prefer the paired server or `tests/server/` Vitest file while iterating.
- Run architecture, localization, protocol, and parity guards matching the changed seam.
- Finish through root `$woc-qa`; the coordinating agent runs shared build and gate commands.
