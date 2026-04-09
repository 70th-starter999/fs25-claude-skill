# 🚜 FS25 Claude Skill — AI-Powered Mod Development Assistant

[![Release](https://img.shields.io/github/v/release/TheCodingDad-TisonK/fs25-claude-skill?include_prereleases&style=flat-square)](https://github.com/TheCodingDad-TisonK/fs25-claude-skill/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Farming Simulator 25](https://img.shields.io/badge/Farming%20Simulator-2025-green?style=flat-square)](https://www.farming-simulator.com/)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-orange?style=flat-square)](https://claude.ai)

> **"The first definitive Claude skill built specifically for Farming Simulator 25 mod development."**  
> Supercharge your FS25 modding workflow with AI that actually knows the APIs, patterns, and pitfalls.

---

## 🎩 Meet the Experts

When you use this skill, you aren't just talking to a generic AI. You're working with a specialized team:

- **Claude (Senior Software Engineer)**: 🎩 Focuses on technical mandates, Lua 5.1 sandboxing, and high-performance patterns. He ensures your code won't crash the Giants Engine.
- **Samantha (Project Manager)**: 🚀 Keeps your mod project on track, manages repo structure, and ensures you're following the best community standards.

---

## 📖 What Is This?

This is a **Claude Skill** — a modular, self-contained knowledge package that transforms Claude into an expert FS25 developer. It replaces "AI hallucinations" with battle-tested facts.

### The Knowledge Base At A Glance
| Resource | Content | Coverage |
|----------|---------|----------|
| **LUADOC** | 1,661 Documentation Pages | 11,102+ Script Functions |
| **Source** | 267 Giants Lua Files | Internal Engine Implementation |
| **Patterns** | 30+ Validated Templates | GUI, Events, Save/Load, Vehicles |
| **Pitfalls** | 17+ Critical "Crash Traps" | os.time(), DialogElement, goto |

---

## 🎬 Quick Demo

Ask Claude (or me!) anything about FS25 modding:

> 🎩 *"Claude, I need a multiplayer-safe event that syncs a custom 'damageLevel' variable."*  
> 🚀 *"Samantha, what's the correct directory structure for a vehicle specialization mod?"*  
> 🚜 *"How do I create a custom Yes/No dialog that actually works in FS25?"*

---

## 🔧 Technical Mandates (The "Ground Truth")

This skill enforces strict adherence to FS25's unique environment:

1. **Sandboxed Lua 5.1**: No `os.time()`, no `goto`, no `table.pack()`.
2. **Bottom-Left Origin**: GUI coordinates (0,0) are at the bottom-left, not top-left.
3. **Manager Safety**: Always nil-check `g_financeManager`, `g_server`, and `g_client`.
4. **Base Classes**: Use `MessageDialog`, NOT `DialogElement` (it causes white-box rendering crashes).

---

## 📦 Installation & Setup

### 1. Download
Grab the latest `.skill` file from the [Releases](https://github.com/TheCodingDad-TisonK/fs25-claude-skill/releases) page.

### 2. Location
Place the `fs25-modding-skill.skill` file in your project root or your Claude skills folder:
- **Windows**: `%APPDATA%\Claude\skills\`
- **Project**: `/YourModProject/fs25-modding-skill.skill`

### 3. Activate
Restart your Claude session and ask: *"What FS25 modding skills do you have?"*

---

## 📚 Deep Dive: Knowledge Sources

This skill stands on the shoulders of the community's hardest workers:

### 1. FS25 Community LUADOC
Provided by [@umbraprior](https://github.com/umbraprior). Complete API coverage from Engine to Script.
- Found in: `skill/fs25-modding-skill/references/luadoc-index/`

### 2. FS25 Lua Scripting (Source Archive)
Provided by [@Dukefarming](https://github.com/Dukefarming). The actual Giants source code (dataS) for reference.
- Found in: `skill/fs25-modding-skill/references/lua-source-index/`

### 3. FS25 AI Coding Reference (Patterns)
Provided by [@XelaNull](https://github.com/XelaNull) (FS25_UsedPlus). Battle-tested patterns validated against an 83-file production mod with 30+ custom dialogs.
- Source: [XelaNull/FS25_UsedPlus/FS25_AI_Coding_Reference](https://github.com/XelaNull/FS25_UsedPlus/tree/master/FS25_AI_Coding_Reference)
- Found in: `skill/fs25-modding-skill/references/patterns/`, `references/basics/`, `references/advanced/`, `references/pitfalls/`

---

## 🗺️ Roadmap & Community

We're just getting started. Join the effort!

- [x] **v1.0.0** — Initial Release with full 3-way knowledge integration.
- [ ] **v1.1.0** — Giants SDK Official Docs Indexing.
- [ ] **v1.2.0** — `modDesc.xml` Schema Validation Helpers.
- [ ] **v2.0.0** — Specialized Sub-Skills (e.g., "The GUI Expert", "The Vehicle Architect").

### Contributing
Found a new pitfall? Have a pattern that's better than ours? 🎩 Claude and 🚀 Samantha love pull requests! See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## 📄 License

MIT License. Bundled community documentation retains its original licenses from the respective creators. See [LICENSE](LICENSE) for details.

---

<div align="center">

**Made with 🚜 for the FS25 modding community**

*Senior Engineer: Claude · Project Manager: Samantha*

</div>
