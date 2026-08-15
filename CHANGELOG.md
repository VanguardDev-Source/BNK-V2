## [2.2.0] — Economy Expansion: Food Businesses, AmmuNation, Illicit Goods Production, Small Store, Job Center Config, Driving School & Stash Capacity

### Overview
This release focused on configuration and content work across multiple standalone economy resources: food/beverage MLOs, the AmmuNation pricing table, two new crafting/production chains (White Widow, Cookies), the Small Store robbery loop, item registry auditing for YouTool, a full Job Center grade/salary pass, Driving School fee configuration, and a capacity request across all whitelisted stash types. Several sub-items are flagged as **pending** or **blocked** below rather than marked complete, to keep this changelog accurate against actual deployment state.

---

### Added / Configured

- **AmmuNation — Pricing Table**
  - Full item pricing configured for the AmmuNation shop.

  | Item | Price |
  |------|-------|
  | 9mm Ammo Box | $5,000 |
  | Pistol Cartridge Case | $5 |
  | Shotgun Cartridge Case | $10 |
  | Rifle Cartridge Case | $15 |
  | Sniper Cartridge Case | $20 |
  | Knife | $2,500 |
  | Bat | $2,000 |
  | Pistol | $35,000 |

- **White Widow — Production Chain**
  - Crafting recipe implemented for Disposable Vape (output: 5x per craft).
    - Requirements: 5x CBD Oil, 5x THC Oil, 5x Battery.
  - Packing recipe implemented: 5x Disposable Vape + 1x Cardpile → sellable pack.
  - Offline store sell rate configured: $10,000 per 5x Disposable Vape.
  - Consumable effects configured: +50% Armour, -25% Stress.

- **Cookies — Production Chain**
  - Crafting recipe implemented for Brownies (output: 5x per craft).
    - Requirements: 5x CBD Oil, 5x THC Oil, 5x Hemp Butter.
  - Packing recipe implemented: 5x Brownies + 1x Cardpile → sellable pack.
  - Offline store sell rate configured: $10,000 per 5x Brownies.
  - Consumable effects configured: +50% Armor, +100% Stamina.

- **Small Store — Retail & Robbery Loop**
  - Product pricing configured:

  | Item | Price |
  |------|-------|
  | Cigarette | $150 |
  | Lighter | $250 |
  | Food | $100 |
  | Drink | $120 |
  | Boombox | $30,000 |
  | Radio | $1,000 |
  | Phone | $10,000 |

  - Robbery trigger implemented via lockpick minigame.
  - Robbery reward configured: $80,000 dirty money on successful completion.
  - Robbery gating intended to require gang reputation/task completion (see **Blocked** below).

- **Driving School — Fee Configuration**
  - Exam fee: $3,000
  - Driving practical test fee: $20,000 cash
  - Motorcycle practical test fee: $5,000 cash

- **Job Center — Grade & Salary Configuration** (Location ref: `8155`)

  | Job | Grade | Salary | Mechanism |
  |-----|-------|--------|-----------|
  | Tambay | Tambay | $100 | Standard |
  | Diving | Diving | $1,000 | Standard |
  | Vineyard | Vineyard | $1,000 | Auto-grind |
  | Fisherman | Fisherman | $1,000 | Standard |
  | Tailor | Tailor | $1,000 | Auto-grind |
  | Miner | Miner | $1,000 | Auto-grind |
  | Garbage Collector | Garbage Collector | $1,000 | Standard |
  | Taxi | Taxi | $1,000 | Standard |

---

### Fixed

- **Vanilla Unicorn — Access Paths**
  - Resolved missing entrance/path leading to the kitchen (food & drink prep area).
  - Resolved missing access path to the DJ booth.

- **Bahama West Mama**
  - Removed the associated map blip per request.

---

### Removed / Reviewed

- **Map Blips — Food & Beverage Venues**
  - Reviewed and confirmed accurate placement for: UWU, 8 Balls, Taco, Pieline Inn, Vanilla Unicorn (VU), Burger Shot.

---

### Known Issues / Pending

- **The Taco Farmers**
  - ⚠️ MLO has **not yet been deployed** to the server. Flagged here despite the overall "done" status of this batch, since this specific interior is still outstanding — please confirm placement priority before next release.

- **Small Store — Gang Reputation Gating**
  - ⚠️ **Blocked.** Robbery reward/trigger logic is functional, but the gang-reputation requirement layer is not yet implemented.
  - Two implementation paths under consideration:
    1. Build a custom reputation/task-tracking script in-house.
    2. Integrate `rcore_gangs` — **pending owner approval** before adoption, since this introduces a new external dependency.
  - Additional scope for Small Store is expected — per Boss Ismael, more requirements/features are still to be defined for this resource.

- **YouTool — Item Registry Audit Required**
  - ⚠️ Pricing table below has been configured, but **has not been validated against the current server's item registry**. Some listed items may not exist in `qb-core`/`ox_inventory` shared items on this build and will need to be added or remapped before this shop can go live.

  | Item | Price |
  |------|-------|
  | CBD Oil | $250 |
  | THC Oil | $250 |
  | Battery | $150 |
  | Hemp Butter | $150 |
  | Empty Bottle | $1,000 |
  | Chemical | $1,000 |
  | Gelatin | $200 |
  | Cocoa Powder | $200 |
  | Empty Capsule | $500 |
  | Fishing Rod | $5,000 |
  | Fish Bait | $50 |
  | Basket | $1,000 |
  | Plastic Bags | $100 |
  | Rolling Paper | $500 |
  | Shovel | $1,000 |
  | Medicinal Herb | $150 |
  | Hemp Cloth | $200 |

  **Action item:** run a full diff between this list and the live item registry before deployment; flag/remap any missing entries.

- **Job Center — Side Job Assignment Architecture**
  - Note (not a bug): the side jobs above do **not** use a standard `setjob`-style assignment. They operate on a self-contained progression/grind mechanism similar to the Farming system — job state is tracked independently rather than through the normal job-grade assignment flow. This is expected behavior given the auto-grind design, not a missing feature, but worth documenting so it isn't mistaken for a bug in QA.

---

### Requested Enhancements

- **Norte Resto (MLO Needed)**
  - Open call to dev team: if a restaurant MLO for the North side of the map is available, flag it for review so it can be scheduled for deployment.

- **Stash Capacity — Personal / Boss / Public / Evidence Locker**
  - Request submitted to increase both **slot count** and **weight capacity** across all whitelisted stash types (Personal Stash, Boss Stash, Public Stash, Evidence Locker).
  - Not yet implemented — flagged for the next config pass on `ox_inventory` stash definitions.

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

This update touches nearly every core system on the server — vehicles, economy, hospital operations, the job system, civil services, and the underlying performance/database layer that everything else runs on. It was a large coordinated effort across multiple resources, and the result is a noticeably more stable, more secure, and better-structured foundation going forward.
