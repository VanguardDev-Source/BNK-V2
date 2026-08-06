## [2.1.0] — Map Cleanup, Job System Overhaul, City Hall & Farming Integration

### Overview
This pass focused on trimming down map clutter, consolidating the job system down to a fixed, intentional list, standing up a brand-new City Hall resource, and integrating a third-party farming script referenced from an external source video. Several legacy blips, jobs, and apartment locations were fully deprecated as part of this cleanup.

### Removed

- **Map Blip Cleanup**
  - Removed the following blips from the map blip list entirely:
    - Recycle Center
    - Cracking Spot
    - Crafting Zone
    - Diving Area
    - Crop Buyer
    - Farming Supply Store
    - Grapeseed Farm
    - Hunting Zone
    - Jewel Cutting Spot
    - Jewel Vendor
    - Mines
    - Ore Vendor
    - Panning Spot
    - Pawn Shop
    - Police Armoury
    - Sandy Shores Farm
    - Scrap Yard 1
    - Scrap Yard 2
    - Smelting Spot
    - Vineyard
    - Vineyard Processing
    - Washing Spot
    - Weazel News
    - Paleto Bay Greenhouse
  - Blip config table trimmed and re-indexed so removed entries don't leave dangling/empty blip categories on the map legend.

- **Job Center Cleanup**
  - Removed all jobs from the Job Center that are not part of the finalized job list.
  - Job Center now exposes exactly the following roles: **Diving, Vineyard, Hunting, Mining, Tailor, Fishing, Garbage Collector, Taxi**.
  - Removed legacy request ID handling from the Job Center — request ID management has been fully relocated to the new City Hall resource (see below) to keep civilian document processing out of the job assignment flow.

- **Apartment Map Cleanup**
  - Removed all apartment blips/locations from the map with the exception of motels.
  - Removed listings:
    - Del Perro Hts Apartments
    - Richard Majestic Apartments
    - Tinsel Tower Apartments
    - 4 Integrity Way Apartments 1 & 2
  - Motels were intentionally left untouched and remain visible/functional on the map.

### Changed

- **Job List Consolidation**
  - Finalized the active job list to: Diving, Vineyard, Hunting, Mining, Tailor, Fishing, Garbage Collector, Taxi.
  - **Auto-grinding enabled** for Vineyard, Hunting, Mining, and Tailor — these jobs now support automated grind loops rather than requiring fully manual repetition per cycle.
  - Diving, Fishing, Garbage Collector, and Taxi remain manual/interaction-driven jobs (no auto-grind loop applied).

- **City Hall — Map Label**
  - Renamed the map label from **"City Services"** to **"Job Center"** to correctly reflect what that marker now represents, avoiding confusion with the new, separate City Hall location.

### Added

- **City Hall (New Resource)**
  - Stood up a new City Hall interaction point.
  - Coords: `-545.3298, -203.7204, 38.2151, 34.5553`
  - Door lock added to the City Hall entrance.
  - **Change Name** service — allows players to submit a legal name change through City Hall.
  - **Driver's License** — purchase/renewal now handled through City Hall.
  - **Weapon License** — purchase/renewal now handled through City Hall.
  - Request ID processing (previously living in the Job Center) now lives here instead, separating civil document workflows from job assignment.
  - Added a dedicated map blip for City Hall so it's discoverable without prior knowledge of the coordinates.

- **Farming Script Integration**
  - Integrated a third-party farming script (reference: [YouTube — implementation overview](https://www.youtube.com/watch?v=mA0JU9hD1ms)) into the current farming system.
  - Base script hooked into existing planting/harvest events and item registry.
  - ⚠️ **Pending QA** — full function-by-function verification of this script against server framework (event names, callback signatures, and item hooks) is still outstanding and should be treated as **not production-verified** until confirmed. Recommend a dedicated test pass before enabling for all players.

### Notes
- Because Job Center request ID handling moved to City Hall, any external integrations (Discord bots, staff panels) that referenced the old Job Center request ID endpoint will need to be repointed at the City Hall resource.
- Blip and job removals were done at the config level, not just hidden client-side — removed jobs can no longer be selected even via direct command, and removed blips no longer exist in the blip registry.

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
