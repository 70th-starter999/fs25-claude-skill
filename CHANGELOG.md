# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.1.0] - 2026-04-09

### Added
- **3 new pitfalls** in `references/pitfalls/what-doesnt-work.md`:
  - #18: Dialog callback naming conflict — `onClose`/`onOpen` clash with GUI system lifecycle
  - #19: HUD `mouseEvent` — must return `true` when consuming event, or clicks fall through
  - #20: Hook accumulation — `appendedFunction` hooks stack on savegame reload without cleanup
- **New pattern file** `references/patterns/field-detection.md`:
  - Field vs Farmland concepts explained
  - 4-tier player position detection with pcall safety (adopted from FS25_NPCFavor)
  - 3-tier field detection fallback via `g_fieldManager` → farmland → manual iteration
  - Timing warning: `g_fieldManager.fields` is empty at init — delayed retry pattern included
- Updated `SKILL.md` routing table to include the new `field-detection.md` pattern

- **WebFetch integration** for LUADOC and lua-source lookups:
  - `LUADOC-INDEX.md` — updated with base URL + WebFetch instructions; any user can now look up live LUADOC docs without local files
  - `LUA-SOURCE-INDEX.md` — same; live Giants source fetchable via WebFetch
  - `SKILL.md` — steps 2 & 3 now explicitly instruct Claude to use WebFetch
- **New index** `references/ai-coding-reference/AI-CODING-REFERENCE-INDEX.md` — documents all files from XelaNull's FS25 AI Coding Reference with live WebFetch URLs as fallback
- **Fixed attribution** — README.md and SKILL.md now properly credit [@XelaNull](https://github.com/XelaNull) for the pattern/pitfalls/basics/advanced reference files

### Validated In
- FS25_SoilFertilizer v1.5.1.0 (pitfalls #18, #19 from issue #130)
- FS25_SoilFertilizer v1.5+ and FS25_NPCFavor v2.6+ (field detection pattern)

---

## [1.0.0] - 2026-04-06

### 🎉 Initial Release

The first Claude skill for Farming Simulator 25 mod development!

### Added
- **SKILL.md** — Core skill with critical facts, pitfalls, and navigation guide
- **references/basics/** — 4 files covering modDesc, Lua patterns, localization, input bindings
- **references/patterns/** — 14 battle-tested patterns (GUI, Events, Save/Load, Economy, HUD, Shop...)
- **references/advanced/** — 8 advanced topics (Vehicles, Placeables, Triggers, HUD, Animations...)
- **references/pitfalls/** — 17 documented pitfalls from real mod development crashes
- **references/luadoc-index/** — Complete index of 1,661 LUADOC pages with quick lookup guide
- **references/lua-source-index/** — Index of 267 Giants Lua source files with directory guide
- **GitHub repo** — Full documentation, contributing guide, issue templates, CI workflow

### Knowledge Sources Bundled
- FS25_AI_Coding_Reference — patterns validated against 83-file production mod codebase
- FS25-Community-LUADOC index — 11,102+ function coverage
- FS25-lua-scripting index — Full Giants dataS source archive reference

---

## [Unreleased]

### Planned
- Giants SDK official docs integration
- Top 50 community mods index
- Separate specialized sub-skills (GUI, Vehicle, Economy)
- FS22 compatibility notes
