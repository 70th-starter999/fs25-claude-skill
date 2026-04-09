# Using the Community LUADOC with This Skill

The [FS25 Community LUADOC](https://github.com/umbraprior/FS25-Community-LUADOC) by [@umbraprior](https://github.com/umbraprior) is the most complete API reference for FS25. This skill gives Claude direct access to it.

---

## How It Works (v1.1.0+)

The skill includes a **complete categorized index** of all 1,661 LUADOC pages. When you ask Claude about a specific API, it:

1. Finds the correct path in `references/luadoc-index/LUADOC-INDEX.md`
2. Constructs the full raw GitHub URL
3. Uses **WebFetch** to retrieve the live documentation — no local install needed

**Example:** If you ask about `g_gui:loadGui()`, Claude fetches:  
`https://raw.githubusercontent.com/umbraprior/FS25-Community-LUADOC/main/docs/script/GUI/Gui.md`

This means you always get up-to-date docs, and it works for any user anywhere.

---

## Browsing the LUADOC Directly

**Online (easiest):**  
https://fs25-community-luadoc.pages.dev/

**Locally (for offline use):**
```bash
git clone https://github.com/umbraprior/FS25-Community-LUADOC
cd FS25-Community-LUADOC/website
npm install
npm start
# Open http://localhost:3000
```

---

## LUADOC Structure

```
docs/
├── engine/          ← Giants engine APIs (C++ bindings)
│   ├── Animation/
│   ├── Camera/
│   ├── Entity/
│   ├── I3D/
│   ├── Input/
│   ├── Math/
│   ├── Network/
│   ├── Node/
│   ├── Physics/
│   ├── Rendering/
│   ├── Sound/
│   ├── Terrain/
│   ├── XML/
│   └── ...
├── script/          ← Lua game script APIs
│   ├── AI/
│   ├── Animals/
│   ├── Economy/
│   ├── GUI/         ← Most mod-relevant
│   ├── Hud/
│   ├── Placeables/
│   ├── Specializations/
│   ├── Utils/
│   ├── Vehicles/
│   └── ...
└── foundation/      ← Core Lua extensions
```

---

## Most Used Pages (Bookmark These)

| What you're doing | LUADOC page |
|-------------------|-------------|
| Creating a custom dialog | `docs/script/GUI/Gui.md` + `docs/script/GUI/MessageDialog.md` |
| Adding buttons | `docs/script/GUI/ButtonElement.md` |
| Text display | `docs/script/GUI/TextElement.md` |
| Text input field | `docs/script/GUI/TextInputElement.md` |
| Dropdown selector | `docs/script/GUI/MultiTextOptionElement.md` |
| Layout containers | `docs/script/GUI/BoxLayoutElement.md` |
| Scrollable list | `docs/script/GUI/ListElement.md` |
| Overwriting/appending functions | `docs/script/Utils/Utils.md` |
| Farm money | `docs/script/Economy/FarmManager.md` |
| Reading/writing XML | `docs/engine/XML/` |
| Node positions | `docs/engine/Node/` |
| Sounds | `docs/engine/Sound/` |
| Physics | `docs/engine/Physics/` |
| Vehicle specializations | `docs/script/Specializations/` |
| HUD elements | `docs/script/Hud/` |
| Trigger zones | `docs/script/Triggers/` |
| Field / farmland system | `docs/script/Field/FieldManager.md` |

---

## Tips

- **Function not found?** Search the LUADOC website — it's full-text searchable
- **Confused about parameters?** Ask Claude — it will WebFetch the exact signature for you
- **Giants source?** Ask Claude to check the lua-scripting source too — sometimes the implementation reveals things the docs don't
- **Offline?** Clone the repo and run locally — it's a static Docusaurus site
