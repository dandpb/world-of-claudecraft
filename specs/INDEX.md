# Allium specs for World of ClaudeCraft

Distilled from `src/`, `server/`, and `docs/` via the Allium `distill` skill. Each
file is a behavioural hypothesis extracted from code; validate against stakeholders
before treating as authoritative. Every spec passes `allium check` with 0 findings
(info-level `unreachableTrigger` / `field.unused` notices on external command triggers
and data-shape fields are inherent and expected).

## Wave 1 - core + game systems
- [done] `deterministic-sim-core.allium` - the 20 Hz tick, seeded-Rng contract, entity lifecycle, one-sim-three-hosts boundary, determinism and purity invariants.
- [done] `combat.allium` - hit table, damage, armor DR, auras, area-echo charges, crowd-control diminishing returns.
- [done] `classes-talents.allium` - 9 classes, specs, talent choice rows, spec commitment, respec, grant-only signature rule, the v0.28 baseline floor.
- [done] `professions.allium` - crafting, the single-draw masterwork proc, production-wheel archetype identity, recipe acquisition and grandfathering, the identity journey.
- [done] `items-loot-equipment.allium` - item instances, deterministic loot rolling, corpse loot rights, equipment slots, set bonuses, salvage, enchant/disenchant.

## Wave 2 - PvE/PvP content + economy + deeds + social
- [done] `dungeons-raids-delves.allium` - instances, heroic lockouts, the Nythraxis raid, delves, the lockpick minigame, mythic+ keystone ladder, forged drops.
- [done] `pvp-honor.allium` - PvP hostility flags, honor with anti-farm DR, arena Elo, fiesta/vale-cup, the Frontier two-loops and $WOC token firewall.
- [done] `economy-bank.allium` - bank vault and entitlements, copper/honor currencies, Claudium soft currency, wallet linking, the $WOC firewall (note: "cargo" is not a currency in code).
- [done] `deeds-achievements.allium` - deeds catalog, the deterministic evaluator pipeline, Renown, the cosmetic-only invariant.
- [done] `social-guilds-party.allium` - friends (one-directional auto-add), blocks, guilds, party/raid group, party credit-sharing, mail with attachment escrow.

## Wave 3 - server authority + online services
- [done] `server-authority.allium` - the GameServer authoritative loop, wire protocol, ClientWorld mirror, interest scoping, reconnect, the client-never-decides invariant.
- [done] `auth-accounts.allium` - REST auth, accounts, sessions, OAuth/Apple/GitHub/Discord, desktop login, character selection, Steam-as-mirror.
- [done] `rest-pipeline.allium` - RouteDef registry, onion middleware, two-tier rate limiting, RFC 9457 error envelope, BOLA ownership, append-only code catalog.
- [done] `moderation-admin.allium` - admin runtime and permissions, jail gate, bug reports, two-tier chat filter, anti-bot, the ALLOW_DEV_COMMANDS gate.
- [done] `quests-progression.allium` - quest lifecycle and objective credit, leveling on a classic XP curve, daily rewards.

## Wave 4 - presentation + cross-cutting
- [done] `hud.allium` - HUD windows (cast bar, action bar, unit frames, quest tracker, chat, loot), HudContext seam, per-frame write elision, the gameplay-neutral graphics-fairness invariant.
- [done] `i18n.allium` - the `t()` contract, sparse-overlay catalog, two-tier gate, lazy locales, the S3 sim-text re-localization flow.

## Cross-spec notes
- The single deterministic `Rng` stream and pinned draw order recur across specs (combat, professions, items, dungeons); each pins it locally as an invariant.
- Server authority (client never decides outcomes) is the boundary spec `server-authority.allium`; game-system specs model the sim behaviour and reference that boundary.
- The `$WOC` token firewall recurs in `economy-bank` and `pvp-honor`; both model the sim vocabulary ending at cargo/honor/copper.
- Terminology is unified per the distill rule (one name per concept); any code duplicate flagged as debt in the spec's Excludes or an open question. Corrections found during distill are recorded as open questions (e.g. friends is auto-add, cargo is not a currency).
- After distillation, the loop continues: validate specs with stakeholders, then `propagate` tests from each, then `weed` spec-vs-code drift.
