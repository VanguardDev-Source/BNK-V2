# Production Changelog — Hospital, Gameplay, Security & Business Expansion

> **Release Status:** Production Update  
> **Scope:** Hospital systems, player capacity, consumable effects, anti-cheat, gang systems, NPC behavior, Meth Lab, and Business Creator expansion.

## Status Legend

| Status | Meaning |
|---|---|
| ✅ Completed | Implemented and considered done |
| 🔎 Verification | Implemented; final in-game verification requested |
| 🟡 Escalated | Forwarded to the relevant script creator/developer |

---

# 🏥 Hospital System

## 1. Removed Hospital Clock-In / Clock-Out Interaction

**Status:** ✅ Completed

Removed the unnecessary Clock In / Clock Out interaction from the hospital area.

**Location removed:**
```text
X: 311.1200
Y: -596.8934
Z: 43.2841
Heading: 157.9832
```

### Changes
- Removed the Clock In / Clock Out interaction.
- Eliminated the unnecessary duplicate interaction point.
- Cleaned up the hospital employee interaction flow.

---

## 2. Hospital Check-In Relocation

**Status:** 🔎 Verification

The hospital Check-In interaction was relocated.

### Previous Location
```text
X: 308.4753
Y: -595.5840
Z: 43.2841
Heading: 90.0884
```

### New Location
```text
X: 306.6097
Y: -594.8839
Z: 43.2841
Heading: 243.1844
```

### Additional Improvements
- Added a **visible map blip** for all players.
- Reworked the interaction for easier discovery.
- Preferred interaction method is the **`E` key**.

---

# 👥 Server Capacity

## 3. Increased Maximum Player Capacity

**Status:** ✅ Completed

Updated the server maximum capacity to:

```text
64 Players
```

The server is now configured to support up to 64 concurrent players.

---

# 🍪 Cookies / Whitewidow Businesses

## 4. Offline Store Disabled

**Status:** 🔎 Verification

Temporarily disabled the offline-store functionality for:

- Cookies
- Whitewidow

### Intended Behavior
```text
Offline Store: DISABLED
```

This prevents the businesses from continuing to operate through the offline-store functionality while related effects and item behavior are finalized.

---

## 5. Consumable Effects & Item Behavior

**Status:** 🔎 Verification

Updated the Cookies / Whitewidow consumable behavior.

### Implemented Requirements
- Added/fixed missing item icons.
- Added gameplay effects without visual effects.
- Addressed Brownies and vape-related effects.
- Consumables can be used while the player is holding a weapon.
- Consumable usage does **not cancel sprinting**.
- Effects operate without unnecessary visual overlays.

### Business Configuration

Business locations can be configured through:

```text
/businesscreator
```

Current development scope focuses on:
1. Item icons
2. Consumable effects
3. Usage behavior
4. Offline-store disabling

---

# 👁️ First-Person POV

## 6. First-Person Camera Fix

**Status:** ✅ Completed

Resolved the issue where First-Person POV was not functioning correctly.

### Result
- First-Person camera functionality restored.
- Players can properly use the First-Person perspective.

---

# 🍫 Brownies

## 7. Brownie Consumable Functionality

**Status:** 🔎 Verification

Addressed the previously non-functional Brownies system.

### Updated
- Brownie item behavior.
- Consumable effects.
- Compatibility with the updated consumable system.

### Verification
- [ ] Item can be consumed.
- [ ] Effect activates correctly.
- [ ] No unintended visual effects are displayed.
- [ ] Sprinting remains available.
- [ ] Weapon-held usage works where intended.

---

# 🧪 MDscript — Meth Lab

## 8. Meth Lab Interior Prop Expansion

**Status:** 🔎 Verification

Expanded the Meth Lab interior environment through **MDscript**.

### Development Scope
- Meth Lab environmental props.
- Grinding-related tables.
- Associated Meth Lab functions.
- Interior interaction/environmental expansion.

### Previous Issue
The previous update contained Meth Lab tables/objects and related functions, but the implementation was not functioning correctly.

### Verification
- [ ] Props spawn correctly.
- [ ] Props persist after resource/server restart.
- [ ] Grinding tables are accessible.
- [ ] Associated functions execute correctly.
- [ ] No script errors occur during interaction.

---

# 🛡️ Anti-Cheat / VG Security

## 9. Anti-Cheat Integration

**Status:** ✅ Completed

The Anti-Cheat system has been integrated and is operational.

### Commands
```text
/vg
/vgadmin
```

### Implementation
- Anti-Cheat system is present and operational.
- VG / VGAdmin integration is active.
- New permission requirements have been adjusted.

### Administrative Notes
Permission configuration ensures the correct staff/admin roles have access to the appropriate VG and VGAdmin functionality.

---

# 🟣 rcore Gang

## 10. Gang & Vehicle Color Expansion

**Status:** 🟡 Escalated to Script Creator

The existing `rcore_gang` color-selection functionality was reviewed.

### Current Limitation
The current system provides too few color choices for:
- Gang colors
- Gang vehicle colors

### Requested Enhancement
The requirement has been escalated to the script creator for expanded color selection.

### Preferred Implementation

```text
Gang Management
      ↓
Choose Gang Color
      ↓
Color Wheel / Expanded Palette
      ↓
Save Gang Color
```

And:

```text
Gang Vehicle
      ↓
Choose Vehicle Color
      ↓
Color Wheel / Expanded Palette
      ↓
Apply / Save Color
```

### Current Status
Server-side requirement has been identified and escalated to the script creator.

---

# 🚶 NPC Population & Drug-Selling Environment

## 11. Ambient Walking NPCs

**Status:** ✅ Completed

Adjusted NPC behavior to provide a more active street environment.

### Changes
- Added a small number of walking NPCs.
- Removed unnecessary driving NPC behavior.
- Reduced unwanted NPC vehicle activity.
- NPC presence supports the gang drug-selling environment.

---

# 🏢 Business Creator — Additional Props

## 12. Added Meth / Weed Business Props

**Status:** ✅ Completed

Expanded the available object pool for `/businesscreator`.

| Prop | Hash |
|---|---:|
| `sf_prop_sf_weed_med_01a` | `1886870120` |
| `bkr_prop_meth_chiller_01a` | `2352447451` |
| `tr_prop_meth_table01a` | `656091709` |
| `prop_meth_setup_01` | `2235078225` |

### Purpose
These assets expand Business Creator options for:
- Weed-related businesses
- Meth Lab interiors
- Drug-processing environments
- Production tables
- Custom illicit-business interiors

### Reference
```text
https://forge.plebmasters.de/objects?search=meth
```

---

# 🧾 Production Ticket Summary

| # | Module / System | Change | Status |
|---:|---|---|:---:|
| 01 | Hospital | Remove Clock In / Clock Out | ✅ |
| 02 | Hospital | Relocate Check-In | 🔎 |
| 03 | Hospital | Visible Check-In blip for all players | 🔎 |
| 04 | Hospital | Prefer `E` interaction | 🔎 |
| 05 | Server | Increase max players to 64 | ✅ |
| 06 | Cookies | Disable Offline Store | 🔎 |
| 07 | Whitewidow | Disable Offline Store | 🔎 |
| 08 | Cookies / Whitewidow | Consumable effects | 🔎 |
| 09 | Cookies / Whitewidow | Item icons | 🔎 |
| 10 | Consumables | Weapon-held usage support | 🔎 |
| 11 | Consumables | Do not cancel sprint | 🔎 |
| 12 | POV | Fix First-Person camera | ✅ |
| 13 | Brownies | Fix consumable functionality | 🔎 |
| 14 | MDscript | Meth Lab interior props | 🔎 |
| 15 | MDscript | Grinding tables/functions | 🔎 |
| 16 | Anti-Cheat | `/vg` integration | ✅ |
| 17 | Anti-Cheat | `/vgadmin` integration | ✅ |
| 18 | Anti-Cheat | New permissions | ✅ |
| 19 | rcore_gang | Expanded gang colors | 🟡 |
| 20 | rcore_gang | Expanded vehicle colors | 🟡 |
| 21 | NPC | Add walking NPCs | ✅ |
| 22 | NPC | Remove driving NPCs | ✅ |
| 23 | Gang Gameplay | NPC environment for drug selling | ✅ |
| 24 | Business Creator | Add weed prop | ✅ |
| 25 | Business Creator | Add Meth Lab props | ✅ |

---

# 🔍 Final QA / Verification Checklist

### Hospital
- [ ] Clock In / Clock Out interaction is completely removed.
- [ ] Check-In is located at the new coordinates.
- [ ] Check-In blip is visible to all players.
- [ ] `E` interaction works correctly.
- [ ] No duplicate Check-In interaction remains at the old location.

### Cookies / Whitewidow / Brownies
- [ ] Offline Store is disabled.
- [ ] Item icons display correctly.
- [ ] Effects trigger correctly.
- [ ] Effects have no unintended visual effects.
- [ ] Items can be used while holding a weapon where intended.
- [ ] Sprinting is not cancelled.
- [ ] Brownies function correctly.
- [ ] Vape functionality works correctly.

### Meth Lab
- [ ] Interior props load correctly.
- [ ] Grinding tables are present.
- [ ] Associated functions work.
- [ ] No console/resource errors occur.
- [ ] Props remain after reconnect/restart.

### Anti-Cheat
- [ ] `/vg` works for authorized users.
- [ ] `/vgadmin` works for authorized administrators.
- [ ] New permissions are correctly assigned.
- [ ] Unauthorized players cannot access restricted functionality.

### NPC Environment
- [ ] Walking NPCs spawn correctly.
- [ ] Unwanted driving NPCs no longer spawn.
- [ ] NPC behavior does not create excessive server/client load.
- [ ] Gang drug-selling interactions work as intended.

### Business Creator
- [ ] All newly added props appear in the object list.
- [ ] Props can be placed through `/businesscreator`.
- [ ] Props save/load correctly.
- [ ] Meth/weed props have correct models and hashes.

### rcore Gang
- [ ] Script creator receives the expanded color-selection requirement.
- [ ] Gang color wheel/palette is implemented.
- [ ] Vehicle color wheel/palette is implemented.
- [ ] Saved colors persist correctly.

---

# 📌 Deployment Notes

This update represents a multi-system production pass covering:

- Hospital interaction cleanup
- Medical Check-In UX
- Server capacity
- Consumable systems
- Business systems
- Meth Lab environments
- NPC population behavior
- Gang functionality
- Anti-Cheat infrastructure
- Business Creator content expansion

The majority of the changes are implemented. Items marked **🔎 Verification** should receive a controlled in-game QA pass before being considered fully closed. The `rcore_gang` color enhancement remains **🟡 Escalated** to the script creator because the requested expanded color-picker behavior depends on the external resource implementation.
