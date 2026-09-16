# 🚀 Server Development Changelog

> **Release:** Major Gameplay, Economy, Identity & Infrastructure Update  
> **Status:** Production Update  
> **Scope:** Gameplay Systems • Loot Economy • Police • Medical • Identity • Character System • Business System • UI/Client Fixes

---

## 📋 Overview

This release contains a broad set of gameplay improvements, system integrations, economy adjustments, bug fixes, configuration changes, and quality-of-life updates across the server.

The update involved work across multiple resources, including **loot balancing, character data, identity systems, police progression, medical services, business creation, inventory behavior, UI state handling, and vehicle systems**.

> **Overall Status:** 🟢 Major server-side gameplay and systems update completed, with the Hospital Respawn component pending infrastructure/configuration support.

---

# 🏠 House Robbery — ✅ Completed

### Loot & Interaction Improvements

- Completed the **House Robbery system implementation and configuration**.
- Added an automatic **ped bag system** that equips the required bag immediately upon the player's first entry into a robbery location.
- Configured the bag behavior to automatically apply when entering the house.
- Reworked the robbery loot pool to establish clearer progression between common and high-value items.

### Loot Rarity Distribution

| Rarity | Drop Rate |
|---|---:|
| 🟢 **Common** | 50% |
| 🔵 **Uncommon** | 40% |
| 🟣 **Rare** | 15% |
| 🔴 **Very Rare** | 5% |

### Loot Pool Reorganization

- Moved `at_suppressor_heavy` → **Common**
- Moved **all Blueprints** → **Uncommon**
- Moved **all Hacker Loot** → **Rare**
- Moved **all Weapons** → **Very Rare**
- All other loot classifications remain unchanged.

> The loot system was restructured to provide a more consistent rarity hierarchy while preserving the existing items and configurations that were not specifically requested for modification.

---

# 🌿 Weed Farm — ✅ Completed

### Farm Entry Location

Configured the Weed Farm entry point:

```text
-16.6815, -1430.4633, 31.1015, 263.6262
```

### Implementation

- Added/configured the new farm location.
- Integrated the location with the existing Weed Farm system.
- Verified the location configuration and entry point.

---

# 🧪 Meth Lab — ✅ Completed

### Interior Rework

- Reworked the **Meth Lab interior**.
- Removed/disabled the previous non-functional interactions.
- Cleaned up unused functionality from the existing implementation.
- Prepared the interior for the existing Meth Lab workflow without retaining broken interactions.

---

# 🕶️ Black Market — ✅ Completed

### Black Market Location

Configured the Black Market location:

```text
2330.7129, 2573.3511, 46.6801, 335.3342
```

### Trigger Configuration

- Configured the required **Black Market trigger**.
- Integrated trigger identifier:

```text
3057
```

- Troubleshot the previously non-functional Black Market configuration.
- Updated the relevant location and interaction configuration.

---

# 👤 New Character / Starter System — ✅ Completed

### Starter Gift Integration

Newly created characters now receive the configured starter package through:

```text
/regalo 1
```

### Changes

- Integrated the starter reward into the new-character flow.
- Ensured the starter package can be granted immediately after character creation.
- Reduced the need for manual starter-item distribution.

---

# 👮 Police System — ✅ Completed

## NPC Side Job

- Added/configured the **Police NPC Side Job**.
- Integrated the task system with the Police progression/reward structure.

## Police Coin Rewards

Each completed Police task now provides:

```text
5x Police Coin
```

This establishes Police Coins as the dedicated reward currency for the configured Police tasks.

---

# 🔫 Musket — ✅ Completed

### Police Coin Pricing

The Musket purchase price has been changed to:

```text
5,000 Police Coins
```

### Changes

- Updated the weapon economy configuration.
- Converted the purchase requirement to the Police Coin system.
- Applied the new pricing consistently with the Police reward structure.

---

# 📦 Ammunition Boxes — ✅ Completed

### Ammunition Capacity Rework

All ammunition boxes have been standardized to contain:

```text
250x Bullets per Box
```

### Changes

- Updated ammunition-box capacity.
- Standardized the quantity across supported ammo boxes.
- Prevented inconsistent bullet quantities between ammunition box types.

---

# 🏥 Hospital / Medical System — ⚠️ Partially Completed

The requested medical locations and reward structure were prepared/configured. However, the **Hospital Respawn functionality could not be fully implemented** because the current server configuration does not support the required dual-spawn setup.

## Medical Locations

### Doctor / STL Revive

```text
1820.2273, 3675.9617, 34.2748, 296.6193
```

### Doctor Body Bag

```text
-260.7339, 6321.6919, 32.4272, 313.3297
```

## Medical Service Rewards

| Service | Reward |
|---|---|
| 🩹 Heal | Bronze Coin |
| 💉 Revive | Silver Coin |
| 🛍️ Body Bag | Gold Coin |

### Configuration Limitation

The respawn component remains pending because the current medical/server configuration is not configured for the required **two-spawn architecture**.

This is an infrastructure/configuration limitation rather than an issue with the provided coordinates.

---

# 🚓 Vehicle Impound Location — ✅ Completed

The existing vehicle impound location was relocated.

### Previous Location

```text
1649.7100, 3789.6101, 34.7878, 12.4713
```

### New Location

```text
1830.6281, 2541.9055, 45.8842, 263.7599
```

### Changes

- Replaced the previous impound coordinates.
- Updated the corresponding configuration.
- Redirected the existing impound system to the new location.

---

# 🏢 Business Creator — ✅ Completed

### Prop Library Expansion

Expanded the Business Creator with additional production, mechanical, weapons, and business-related props.

| Prop | Hash |
|---|---|
| `gr_prop_gr_lathe_01b` | `0x85635F59` |
| `vw_prop_vw_chipsmachine_01a` | `0x25BFF45F` |
| `prop_rub_carwreck_8` | `0x009A3823` |
| `prop_crosssaw_01` | `0x1055925D` |
| `xm3_int3_weapons_bench` | `0x45F8C9E6` |
| `h4_int_sub_subweaponsmod` | `0x60FE32D5` |
| `m24_1_int_01_m241_wpn_locker` | `0x02F214ED` |

### Creator Improvements

These additions expand the available object library for business owners and administrators, allowing more detailed and specialized business interiors to be created through the Business Creator.

---

# 🪪 Driver's License System — ✅ Completed

### Dealership License Validation

Resolved an issue where players could not purchase vehicles from the dealership despite already having a valid Driver's License.

### Fix

- Corrected the license validation logic.
- Ensured the dealership properly detects an existing valid license.
- Prevented valid license holders from being incorrectly rejected.
- Improved consistency between the player's license data and dealership validation.

---

# 🪪 All ID Systems — ✅ Completed

### ID UI Display Fix

Resolved an issue where IDs could remain stuck on the player's screen after attempting to close them.

### Fix

- Corrected ID UI close behavior.
- Ensured IDs properly disappear after closing.
- Prevented the interface from remaining permanently visible.
- Improved UI state cleanup.

---

# 🏷️ Character Names & ID Visibility — ✅ Completed

### Overhead Name Tag Fix

Resolved an issue where character names and IDs could appear above players regardless of their intended permissions.

### Updated Behavior

- Corrected overhead name/ID visibility.
- Restricted administrative identification functionality to the appropriate permissions.
- Prevented regular citizens from incorrectly receiving administrator-level name/ID displays.
- Improved the permission and visibility logic governing overhead identification.

---

# 🎒 Pocket / Inventory Items — ✅ Completed

### AFK / Sleep Inventory Issue

Investigated and addressed an issue where items could disappear from a player's pocket/inventory after the player became inactive or went AFK.

### Fix

- Addressed inventory persistence behavior.
- Prevented pocket items from incorrectly disappearing during inactivity.
- Investigated the interaction between player state and client-side inventory behavior.

> **Technical Note:** Some remaining occurrences may originate from client-side behavior and may require additional client-side investigation if the issue persists under specific circumstances.

---

# ✂️ Menu / UI Systems — ✅ Completed

### Stuck Menu Fixes

Investigated and corrected menu states that could become stuck in:

- ✂️ Barber / Haircut
- 👕 Clothing
- 🚗 Garage

### Fix

- Corrected menu closing behavior.
- Improved UI state cleanup.
- Prevented menus from remaining active after exiting the associated interaction.
- Improved transitions between interactive menus and normal gameplay.

> **Technical Note:** Some remaining occurrences may be related to client-side behavior depending on the specific circumstances that trigger the issue.

---

# 🪪 Character ID / Gender Detection — ✅ Fixed

### Gender Registration Issue

Resolved a critical issue where **all characters were being registered/displayed as Female**, including characters configured as Male.

### Fix

- Corrected gender retrieval/registration logic.
- Ensured the character's actual gender is correctly passed to the ID system.
- Male characters are now properly registered as **Male**.
- Female characters continue to be registered as **Female**.
- Improved consistency between character appearance data and ID information.

---

# ⏱️ AFK Timer — ✅ Completed

### AFK Timer Removal

Removed the existing AFK Timer functionality as requested.

### Changes

- Disabled the unwanted AFK countdown.
- Removed the player-facing AFK timer behavior.
- Prevented the timer from interfering with normal gameplay.

---

# 👥 Multi-Character System — ✅ Completed

### Character Ownership / Account Linking Fix

Resolved a critical Multi-Character issue where a character could incorrectly become associated with another player's character/account instead of the currently authenticated player.

### Previous Issue Example

A player logged into FiveM as:

```text
Jear Rivaz
```

could incorrectly have a character registered/linked as:

```text
Dani Jackson
```

instead of having the character correctly associated with the authenticated account.

### Fix

- Investigated the character identification and linking process.
- Corrected the account-to-character association logic.
- Ensured characters are linked to the **currently authenticated player/session**.
- Prevented character records from being incorrectly cross-linked between players.
- Improved the reliability of Multi-Character registration and retrieval.
- Addressed potential persistent-data integrity concerns caused by incorrect character associations.

> **Data Integrity:** This fix is particularly important because incorrect character association can potentially affect persistent identity, inventory, ownership, and other player-specific data.

---

# 📊 Change Summary

| System | Status | Scope |
|---|:---:|---|
| House Robbery | ✅ | Loot, bag system, rarity balancing |
| Weed Farm | ✅ | Location configuration |
| Meth Lab | ✅ | Interior/function rework |
| Black Market | ✅ | Location & trigger |
| New Character | ✅ | Starter reward integration |
| Police | ✅ | NPC side job & rewards |
| Musket | ✅ | Police Coin pricing |
| Ammo Boxes | ✅ | 250x bullet capacity |
| Hospital | ⚠️ | Locations/rewards configured; respawn blocked by server configuration |
| Vehicle Impound | ✅ | Location relocation |
| Business Creator | ✅ | Prop library expansion |
| Driver's License | ✅ | Dealership validation |
| ID Systems | ✅ | UI/state fixes |
| Character Names | ✅ | Visibility/permission fixes |
| Pocket Items | ✅ | Persistence investigation/fix |
| Menus | ✅ | Barber, Clothing & Garage |
| Character Gender | ✅ | Male/Female detection fix |
| AFK Timer | ✅ | Removed |
| Multi-Character | ✅ | Account/character linking |

---

# 🔧 Development Scope

This update required work across multiple layers of the server rather than simple configuration edits.

### Areas addressed

- **Gameplay Systems**
- **Loot Tables & Rarity Balancing**
- **Economy & Reward Configuration**
- **Police Progression**
- **Medical Services**
- **Character Creation**
- **Character Ownership**
- **Persistent Player Data**
- **Identity & License Validation**
- **Inventory Behavior**
- **UI State Management**
- **Business Creation**
- **World Locations**
- **Interaction Triggers**
- **Client/Server Troubleshooting**
- **Resource Configuration**
- **Data Integrity**

Several issues required investigation beyond their visible symptoms because their behavior could involve interactions between **client-side logic, server-side logic, persistent player data, resource configuration, and UI state**.

---

# 📝 Final Development Status

### 🟢 Production Ready

The majority of requested gameplay, economy, identity, police, business, inventory, UI, and character-system changes have been implemented and completed.

### 🟡 Pending Infrastructure Support

The **Hospital Respawn** component remains pending due to the current server's lack of support/configuration for the required dual-spawn architecture.

Once the underlying medical/spawn configuration supports multiple spawn points, the remaining hospital respawn behavior can be implemented without requiring the previously configured coordinates to be changed.

---

## 📦 Release Notes

**Total Areas Updated:** 18  
**Primary Categories:** Gameplay • Economy • Police • Medical • Identity • Character Systems • UI • Business • Vehicles

> This release represents a substantial multi-resource development pass focused on improving server functionality, progression, data consistency, player experience, and long-term maintainability.
