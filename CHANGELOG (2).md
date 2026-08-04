# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

This release represents a major overhaul across the economy, vehicle, and hospital/EMS systems — spanning new resource development, core performance optimization, database refactoring, and a full permissions/access-control pass. Below is the complete breakdown.

---

## [2.0.0] — BNK V2

### Overview
This is the largest economy-side update to date. It introduces six new player-facing systems, reworks the weapon reload pipeline, and includes a full performance pass on the qbx_core boot sequence and database layer. Every new resource was built with server-authoritative validation to close off client-side exploit vectors present in earlier iterations.

### Added

- **Modded Cars**
  - Full modded vehicle catalog added to the shared vehicle registry.
  - Custom handling.meta profiles tuned per vehicle class (grip, torque curve, drivetrain).
  - Server-side spawn validation to prevent unauthorized model injection.
  - Vehicle metadata (mods, livery, plate) now persists correctly through garage store/retrieve cycles.

- **Car Dealership**
  - New standalone dealership resource with browsable catalog, test-drive flow, and purchase confirmation UI.
  - Finance/installment purchase path wired into the banking system, with automatic recurring deduction and default-handling logic.
  - Dealership inventory is now database-backed rather than hardcoded, so stock can be adjusted without a resource restart.
  - Added purchase logging for audit/anti-duplication tracking.

- **Pharmacy**
  - New pharmacy resource for medicine purchases (`bilihan ng gamot`).
  - Fully integrated with the shared inventory system and item registry.
  - Stock and pricing are configurable per item, with server-side price validation to prevent client-side price tampering.

- **Farming System (Fruits & Vegetables)**
  - New agriculture gameplay loop: planting, growth-stage timers, watering/maintenance mechanics, and harvest yield.
  - Growth stages are tracked server-side and persist across server restarts (no more lost crops on reboot).
  - Harvested produce is registered as sellable inventory items, feeding directly into the broader economy loop.
  - Added anti-macro/anti-spam throttling on repeated planting actions.

- **Economy — Grindings Trade (Willies, North)**
  - New sell point for grindings at the Willies location, North side of the map.
  - Price validation is fully server-side; client can no longer submit arbitrary sell values.
  - Sell transactions are logged for economy monitoring and inflation tracking.

- **Clothing Store**
  - New clothing store resource with a $1,000 entry/access fee.
  - Entry fee is synced against the player's bank/cash balance with proper insufficient-funds handling.
  - Outfit browsing and preview integrated with the existing clothing/appearance framework.

### Changed

- **Reload System Rework**
  - Reload logic reworked so weapons load a single round per reload cycle instead of a full magazine.
  - Auto-reload has been fully disabled at both the client event layer and the server-side ammo validation layer.
  - This reduces event spam on rapid reload spam-clicking and closes an exploit path where auto-reload could desync ammo counts between client and server.

- **Database Layer Optimization**
  - Optimized the core database connection pooling configuration (oxmysql) to reduce connection churn under concurrent load.
  - Refactored redundant queries fired during the qbx_core boot sequence — several player-load queries were being executed more than once per session due to overlapping event handlers.
  - Eliminated duplicate player-load callbacks that were firing on resource restart, which had been silently doubling up on inventory/metadata hydration.
  - Query batching introduced where multiple related lookups previously fired as separate round-trips.

- **Resource Performance Pass**
  - Profiled qbx_core and its dependent resources under both idle and peak-load conditions.
  - Consolidated several polling loops into event-driven callbacks, cutting unnecessary server tick overhead.
  - Idle resource monitor (`resmon`) footprint reduced and stabilized at **~0.45ms** on server idle — previously subject to spikes caused by unoptimized loops and redundant tick handlers running even when no players were interacting with affected systems.
  - Verified stability under simulated concurrent player load with no regression in idle baseline after warm-up.

### Removed

- **Local NPCs/Vendors** ("mga lokal")
  - Removed legacy local vendor peds and their associated ped-spawn/despawn loop from the map.
  - Cleaned up orphaned ped handles that were previously left behind on resource restart, contributing to memory creep over long uptime sessions.

### Fixed

- **Map Postal/Address Labels**
  - Added missing postal/address markers across the map.
  - Resolved a mismatch between the GPS lookup table and the in-game postal display that had been causing incorrect address results for dispatch and delivery-based systems.

---

## [1.4.0] — HP (Hospital / EMS System)

### Overview
A full rebuild of the Hospital/EMS workflow — from clock-in through payroll-adjacent Gold Coin economy, to physical access control across the building. Every interaction point below was re-scoped, and several were relocated or replaced outright based on internal review of the previous layout. Access control is now grade-based and enforced server-side rather than relying on client trust or job-name string matching.

### Added

- **Ambulance Documents**
  - New interactable documents point at the ambulance bay for reviewing/handling ambulance paperwork.
  - Coords: `311.0559, -593.8194, 43.2841, 8.1889`

- **Clock In / Clock Out System**
  - Full time-tracking flow implemented, replacing the old check-in point entirely.
  - Coords: `308.2586, -595.5312, 43.2841, 66.1533`
  - Discord webhook integration logs every clock-in and clock-out event automatically.
  - Webhook payload includes: `Name`, `Date`, `Time`, `Total Hours (Clock Out)`.
  - Logging is handled server-side through `qbx_core` job event hooks, so clock times cannot be spoofed or edited client-side.
  - Total hours are calculated server-side at clock-out based on the stored clock-in timestamp, avoiding client clock drift issues.

- **Public Stash**
  - New shared EMS stash added to replace the old personal stash model.
  - Coords: `307.0923, -601.9344, 43.2855, 163.8375`

- **Armory Relocation & Re-Stock**
  - Armory moved to a new, more secure position.
  - New coords: `311.9856, -597.6472, 43.2841, 163.2946`
  - Stocked items: Radio, First Aid, Flashlight.
  - Removed from the armory loadout: Bandage, Painkillers, Fire Extinguisher — consolidating consumables into the medical bag/stash flow instead of the armory.

- **Gold Coin Economy**
  - Full coin-based currency exchange and automatic payout system implemented.
  - NPC exchange: 1 Gold Coin → $7,000 clean money + 1 EMS Token.
  - Exchange NPC coords: `310.3437, -602.9509, 43.2841, 258.2772`
  - Auto-payout of 1 Gold Coin to EMS inventory is triggered on: Treatment, Heal, Revive, and Bodybag actions.
  - Payout logic is tied directly to the medical action's server-side completion callback, rather than a client-fired event, preventing duplicate/farmed payouts.

- **Surgery Card & EMS Token Stash**
  - New restricted stash, gated by ACE permissions to Director and Surgeon grades only.
  - Coords: `339.2131, -595.6033, 43.2841, 257.0698`
  - Unauthorized access attempts are rejected server-side with no client-visible stash contents leaking on failed permission checks.

- **Director's Office**
  - Full management terminal added, consolidating what were previously separate/manual processes into one interface: stash access, employee management, hire, promote/demote, and department funds.
  - Coords: `334.8803, -594.0164, 43.2841, 243.3293`

- **Garage Elevator**
  - New elevator connecting the main floor to the basement garage, which was previously unreachable in-game.
  - Coords: `340.0220, -584.7617, 28.7968, 250.8629`

- **Ambulance Garage**
  - New garage blip and dedicated vehicle spawn point.
  - Blip: `334.3929, -589.9601, 28.7968, 104.2121`
  - Spawn: `326.5609, -587.5596, 28.7969, 341.2110`

- **Doorlocks**
  - Access-controlled doorlocks configured across all 8 points below, gated to on-duty EMS staff.

  | # | X | Y | Z | Heading |
  |---|-----------|-----------|---------|----------|
  | 1 | 304.6496 | -572.0143 | 43.2841 | 68.6409 |
  | 2 | 307.6701 | -570.2552 | 43.2841 | 354.4564 |
  | 3 | 312.9974 | -572.0152 | 43.2844 | 326.1657 |
  | 4 | 318.9099 | -574.1493 | 43.2844 | 329.6105 |
  | 5 | 324.3198 | -576.1339 | 43.2849 | 350.4920 |
  | 6 | 337.7209 | -592.4087 | 43.2841 | 165.3940 |
  | 7 | 313.6421 | -596.2749 | 43.2841 | 76.2725 |
  | 8 | 308.4510 | -597.1889 | 43.2845 | 167.2913 |

- **Greenzone**
  - Greenzone protection enabled around the hospital area.
  - Players inside the zone are immune to damage from attackers outside the boundary.
  - Ragdoll is disabled within the zone, preventing forced-ragdoll griefing at the hospital entrance.

### Changed

- **Change Clothes Menu**
  - Removed the "Buy Clothing" option from the interaction menu; the menu now handles outfit switching only, in line with the new dedicated Clothing Store resource.
  - Coords: `302.0490, -599.1716, 43.2834, 255.4009`

- **Job Roles & Salaries**
  - Configured grade-based salary tiers, replacing the previous flat/manual pay structure.

  | Grade | Role | Salary |
  |-------|------|--------|
  | 0 | Intern | $4,000 |
  | 1 | Nurse | $5,000 |
  | 2 | Surgeon | $6,000 |
  | 3 | Director | $7,000 |

### Removed

- **Check-In Point**
  - Removed the legacy check-in interaction entirely, fully superseded by the Clock In / Clock Out system.
  - Coords: `308.3583, -595.5432, 43.2840, 80.1528`

- **Personal Stash**
  - Removed the old individual stash location, superseded by the new Public Stash.
  - Coords: `307.0923, -601.9344, 43.2855, 163.8375`

---

## Performance Summary

| Metric | Before | After |
|--------|--------|-------|
| Idle `resmon` (qbx_core + dependents) | Variable, spikes under load | Stable at **~0.45ms** |
| DB connection handling | Unpooled, redundant query paths | Pooled, deduplicated, batched |
| Player-load callback firing | Duplicate on resource restart | Single, idempotent load |
| Reload event volume | Multi-round batch triggers | Single-round, throttled |
| Armory/stash access control | Trust-based / job-name checks | ACE permission + grade-based |
| Clock-in/out integrity | N/A (did not exist) | Server-authoritative, webhook-logged |

---

## Migration & Access Notes

- All coordinates follow the `x, y, z, heading` (vector4) convention and were verified against the live server prior to deployment.
- Webhook logging for Clock In/Out is entirely server-authoritative — no webhook URL is exposed to the client at any point.
- Restricted stash and office access is enforced via job grade combined with ACE permissions rather than job-name string matching, so access rules remain stable even if role names are changed or renamed in the future.
- Players with items/cash tied to the old Personal Stash or Check-In systems should be migrated to the new Public Stash and Clock In/Out flow before those legacy resources are fully decommissioned.
- Recommend a full server restart (not just resource restart) after deployment to ensure the database connection pool re-initializes cleanly.

---

## Summary

This update touches nearly every core system on the server — vehicles, economy, hospital operations, and the underlying performance/database layer that everything else runs on. It was a large coordinated effort across multiple resources, and the result is a noticeably more stable, more secure, and better-structured foundation going forward.
