# Developer Changelog

All notable changes to the server are documented in this file.
Format loosely based on [Keep a Changelog](https://keepachangelog.com/).

Legend: 🆕 Added · 🔧 Changed · ❌ Removed · 🐛 Fix Requested · 📌 To-Do

---

## [Unreleased] — BNK V2

### 🆕 Added
- **Modded Cars** — new modded vehicle catalog.
- **Car Dealership** — new vehicle sales system/location.
- **Pharmacy** — new store for purchasing medicine (`bilihan ng gamot`).
- **Farming (Fruits & Vegetables)** — new agriculture gameplay loop for growing/harvesting produce.
- **Economy — Grindings Trade (Willies, North)** — new sell point for "grindings" at Willies, North side of map.
- **Clothing Store** — new store, entry/registration fee of **$1,000**.

### 🔧 Changed
- **Reload System** — reload now loads **one bullet at a time**; **auto-reload has been disabled**.

### ❌ Removed
- **Local NPCs/Vendors** ("mga lokal") — removed from the map per request.

### 🐛 Known Issues
- **Map Postal/Address Labels** — the map currently has no postal (address) markers/labels. Needs implementation.

---

## [Unreleased] — HP (Hospital / EMS System)

### 📌 To-Do List

| # | Task | Status |
|---|------|--------|
| 1 | Remove Check-In point | Pending |
| 2 | Add Ambulance Documents interaction | Pending |
| 3 | Implement Clock In / Clock Out + webhook logging | Pending |
| 4 | Remove old Personal Stash location | Pending |
| 5 | Add Public Stash location | Pending |
| 6 | Remove "Buy Clothing" option from Change Clothes menu | Pending |
| 7 | Relocate & re-stock Armory | Pending |
| 8 | Convert NPC exchange to Gold Coin system | Pending |
| 9 | Implement Gold Coin payout on medical actions | Pending |
| 10 | Add Surgery Card & EMS Token stash (restricted access) | Pending |
| 11 | Build out Director's Office functions | Pending |
| 12 | Add elevator to Garage/Basement | Pending |
| 13 | Set up Ambulance Garage (blip + spawn) | Pending |
| 14 | Configure doorlocks (8 doors) | Pending |
| 15 | Enable Greenzone (no damage/no ragdoll) | Pending |
| 16 | Configure job roles & salaries | Pending |

---

### 1. Check-In — Removal
❌ **Remove** check-in point.

| X | Y | Z | Heading |
|---|---|---|---------|
| 308.3583 | -595.5432 | 43.2840 | 80.1528 |

---

### 2. Ambulance Documents
🆕 **Add** ambulance documents interaction point.

| X | Y | Z | Heading |
|---|---|---|---------|
| 311.0559 | -593.8194 | 43.2841 | 8.1889 |

---

### 3. Clock In / Clock Out
🆕 **Add** clock in/out point, integrated with a webhook for time logging.

| X | Y | Z | Heading |
|---|---|---|---------|
| 308.2586 | -595.5312 | 43.2841 | 66.1533 |

**Webhook log fields:**
- `Name:`
- `Date:`
- `Time:`
- `Total Hours (on Clock Out):`

---

### 4. Personal Stash
❌ **Remove** existing location.

| X | Y | Z | Heading |
|---|---|---|---------|
| 307.0923 | -601.9344 | 43.2855 | 163.8375 |

---

### 5. Public Stash
🆕 **Add** new location.

| X | Y | Z | Heading |
|---|---|---|---------|
| 307.0923 | -601.9344 | 43.2855 | 163.8375 |

---

### 6. Change Clothes
🔧 **Location**

| X | Y | Z | Heading |
|---|---|---|---------|
| 302.0490 | -599.1716 | 43.2834 | 255.4009 |

**Issue:** Menu currently includes a "Buy Clothing" option.
**Request:** Remove the "Buy Clothing" option from this menu.

---

### 7. Armory
❌ **Remove old location**

| X | Y | Z | Heading |
|---|---|---|---------|
| 310.3536 | -602.7875 | 43.2841 | 233.2021 |

🆕 **Move to new location**

| X | Y | Z | Heading |
|---|---|---|---------|
| 311.9856 | -597.6472 | 43.2841 | 163.2946 |

**Items to keep/add:** Radio, First Aid, Flashlight
**Items to remove:** Bandage, Painkillers, Fire Extinguisher

---

### 8. NPC — Currency Exchange
🔧 **Change to coin-based exchange**

| X | Y | Z | Heading |
|---|---|---|---------|
| 310.3437 | -602.9509 | 43.2841 | 258.2772 |

**Exchange rate:**
- 1 Gold Coin = **$7,000 clean money** + **1 EMS Token**

---

### 9. Gold Coin — Earning Logic
🆕 EMS staff receive **1 Gold Coin** into their pocket for each of the following actions:
- Treatment
- Heal
- Revive
- Bodybag

---

### 10. Surgery Card & EMS Token Stash
🆕 **Add** restricted stash.

| X | Y | Z | Heading |
|---|---|---|---------|
| 339.2131 | -595.6033 | 43.2841 | 257.0698 |

**Contents:** Surgery Card, EMS Token
**Access:** Directors and Surgeons only

---

### 11. Director's Office
🆕 **Add** office with the following functions:

| X | Y | Z | Heading |
|---|---|---|---------|
| 334.8803 | -594.0164 | 43.2841 | 243.3293 |

**Functions:**
- Stash
- Management
- Hire
- Promote / Demote
- Funds

---

### 12. Elevator (Garage Access)
🐛 **Issue:** No elevator currently leads to the basement/garage.
🆕 **Add** garage elevator:

| X | Y | Z | Heading |
|---|---|---|---------|
| 340.0220 | -584.7617 | 28.7968 | 250.8629 |

---

### 13. Ambulance Garage
🆕 **Add** blip and vehicle spawn point.

| Type | X | Y | Z | Heading |
|------|---|---|---|---------|
| Blip | 334.3929 | -589.9601 | 28.7968 | 104.2121 |
| Spawn | 326.5609 | -587.5596 | 28.7969 | 341.2110 |

---

### 14. Doorlocks
🆕 **Configure locks** at the following 8 points:

| # | X | Y | Z | Heading |
|---|---|---|---|---------|
| 1 | 304.6496 | -572.0143 | 43.2841 | 68.6409 |
| 2 | 307.6701 | -570.2552 | 43.2841 | 354.4564 |
| 3 | 312.9974 | -572.0152 | 43.2844 | 326.1657 |
| 4 | 318.9099 | -574.1493 | 43.2844 | 329.6105 |
| 5 | 324.3198 | -576.1339 | 43.2849 | 350.4920 |
| 6 | 337.7209 | -592.4087 | 43.2841 | 165.3940 |
| 7 | 313.6421 | -596.2749 | 43.2841 | 76.2725 |
| 8 | 308.4510 | -597.1889 | 43.2845 | 167.2913 |

---

### 15. Greenzone
🆕 Enable greenzone protection for the hospital area:
- Players cannot take damage from outside the zone.
- Ragdoll is disabled within the zone.

---

### 16. Job Roles & Salaries

| Grade | Role | Salary |
|-------|------|--------|
| 0 | Intern | $4,000 |
| 1 | Nurse | $5,000 |
| 2 | Surgeon | $6,000 |
| 3 | Director | $7,000 |

---

## Notes for Implementation Team
- Coordinates are assumed to be `x, y, z, heading` format (standard FiveM `vector4`-style ordering) — please confirm against your framework's coordinate convention before deploying.
- Webhook integration for Clock In/Out (Item 3) will need a Discord (or equivalent) webhook URL and an event trigger on both clock-in and clock-out actions.
- Access control for Item 10 (Surgery Card & EMS Token stash) should be tied to job grade (Director/Surgeon) rather than job name alone, in case grade names change later.
