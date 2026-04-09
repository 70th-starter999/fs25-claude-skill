# FS25 AI Coding Reference — Index

**Source:** [FS25_UsedPlus/FS25_AI_Coding_Reference](https://github.com/XelaNull/FS25_UsedPlus/tree/master/FS25_AI_Coding_Reference) by [@XelaNull](https://github.com/XelaNull)  
**Coverage:** 70+ patterns · 9,000+ lines · Battle-tested against 83-file production mod (FS25_UsedPlus)

**Base URL:** `https://raw.githubusercontent.com/XelaNull/FS25_UsedPlus/master/FS25_AI_Coding_Reference/`

> **How to use:** The pattern files from this reference are included locally in this skill under `references/patterns/`, `references/basics/`, `references/advanced/`, and `references/pitfalls/`. Read those directly.
>
> If you need a fresher version than what's bundled, or a file that isn't bundled, use **WebFetch**:
> `BASE_URL + path`
>
> **Example:**
> `patterns/gui-dialogs.md` → WebFetch `https://raw.githubusercontent.com/XelaNull/FS25_UsedPlus/master/FS25_AI_Coding_Reference/patterns/gui-dialogs.md`

---

## What's Covered

### `basics/`
| File | Topic |
|------|-------|
| `basics/modDesc.md` | modDesc.xml structure, required fields, source file registration |
| `basics/lua-patterns.md` | Core Lua patterns, class system, FS25 idioms |
| `basics/localization.md` | i18n, translation files, g_i18n usage |
| `basics/input-bindings.md` | Key bindings, action registration |

### `patterns/` (Most Valuable ⭐)
| File | Topic |
|------|-------|
| `patterns/gui-dialogs.md` | Custom dialog creation — MessageDialog base, profiles, XML layout |
| `patterns/events.md` | Multiplayer network events — writeStream/readStream, sendToServer |
| `patterns/save-load.md` | Savegame persistence — XML read/write |
| `patterns/managers.md` | Singleton manager pattern |
| `patterns/extensions.md` | Hooking existing classes with Utils.appendedFunction |
| `patterns/data-classes.md` | Data classes with business logic |
| `patterns/financial-calculations.md` | Loans, depreciation, collateral |
| `patterns/async-operations.md` | Deferred/queued operations |
| `patterns/message-center.md` | Event subscription via g_messageCenter |
| `patterns/physics-override.md` | Modifying physics properties |
| `patterns/shop-ui.md` | Shop screen customization |
| `patterns/placeable-purchase-hooks.md` | Custom purchase dialogs |
| `patterns/vehicle-info-box.md` | Vehicle HUD info box |

### `advanced/`
| File | Topic |
|------|-------|
| `advanced/vehicles.md` | Vehicle specializations |
| `advanced/placeables.md` | Placeable objects |
| `advanced/triggers.md` | Trigger zones |
| `advanced/hud-framework.md` | HUD displays |
| `advanced/animations.md` | Animations |
| `advanced/animals.md` | Animal husbandry |
| `advanced/production-patterns.md` | Production chains |
| `advanced/vehicle-configs.md` | Vehicle configurations |

### `pitfalls/`
| File | Topic |
|------|-------|
| `pitfalls/what-doesnt-work.md` | 17 validated crash traps — os.time, DialogElement, Slider, etc. |
