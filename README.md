# ⚔️ WeaponForge

A mobile-first, single-page web app that lets kids design custom **Minecraft Bedrock** weapon skins, set weapon stats, manage multiple weapons in a project, and export a valid `.mcaddon` file they can import directly into Minecraft on iOS.

Built as a fun project with no build tools — just open `index.html` in a browser, or visit the [GitHub Pages site](https://ipfleger.github.io/weaponForge/).

---

## ✨ Features

- **16×16 Pixel Art Editor** — Pencil, Eraser, Flood-Fill, Eyedropper, Lighten, and Darken tools
- **Color Picker** — iro.js wheel with value + alpha sliders; pinned color swatch strip
- **Onion Skin Tracing** — Load vanilla Minecraft tool textures as semi-transparent guides
- **Weapon Stats Panel** — Set display name, weapon type, damage, attack speed, durability, repair material, and off-hand toggle
- **Project Management** — Create, save, and load multiple projects (persisted in IndexedDB)
- **⚒️ Recipe Builder** — Design crafting recipes for your custom weapons using a 3×3 crafting grid; search/browse 300+ vanilla Minecraft items and place your custom weapons in the grid; recipes are saved with the project and exported as Bedrock recipe JSON
- **`.mcaddon` Export** — Generates a valid Bedrock add-on ZIP with resource pack, behavior pack, manifests, textures, item JSONs, and crafting recipe JSONs
- **Post-Export Guide** — Shows iOS import instructions and `/give` commands for each weapon
- **Mobile-First** — Designed for iPhone SE through iPhone 15 Pro Max; works when added to the home screen

---

## 🚀 How to Use

### Open the App
1. Go to `https://ipfleger.github.io/weaponForge/` in Safari on iOS, **or**
2. Download `index.html` and open it directly in any browser (no server needed)

### Create a Weapon
1. Tap **+ New Weapon** on the home screen
2. Draw your weapon texture on the 16×16 canvas using the radial tool menu (bottom-left ⊕ button)
3. Scroll down to fill in the weapon stats (name, type, damage, etc.)
4. Tap **💾 Save** or **← Back** to return to the home screen

### Manage Your Project
- **Tap** a weapon card to edit it
- **Long-press** a weapon card (hold 0.6 s) to delete it
- **💾 Save Project** — persists your project to IndexedDB so it survives page reloads
- **📂 Load Project** — switch between saved projects
- **🗑️ New Project** — start fresh

### Export to Minecraft
1. Tap **📦 Export .mcaddon** on the home screen
2. The browser will download a `YourProjectName.mcaddon` file
3. **On iOS:** tap the downloaded file → tap **Share** → **Open in Minecraft**  
   *(or save to Files app first, then open it)*
4. Minecraft will import both the resource pack and behavior pack automatically

### Design a Crafting Recipe
1. Tap **⚒️ Recipe Builder** on the home screen
2. Browse or search the item grid (300+ vanilla Minecraft items + your custom weapons)
3. Tap an item to select it, then tap a slot in the 3×3 crafting grid to place it
4. Tap the **Result** slot to set the crafting output (place your custom weapon here)
5. Tap **💾 Save** — the recipe is stored with your project
6. Long-press a filled slot (or right-click on desktop) to remove an item from it
7. Export your `.mcaddon` to include the recipe as a Bedrock `behavior_pack/recipes/*.json` file

### Use Your Weapons In-Game
After importing, enable both the resource pack and behavior pack in your Minecraft world settings. Then use the `/give` command shown in the export modal, e.g.:

```
/give @s weaponforge:fire_sword
```

---

## 🗂️ Bedrock Add-On Format

The exported `.mcaddon` is a ZIP archive with this structure:

```
YourProject.mcaddon
├── resource_pack/
│   ├── manifest.json          — Pack metadata & UUIDs
│   ├── pack_icon.png          — 256×256 icon (scaled from first weapon texture)
│   └── textures/
│       ├── item_texture.json  — Texture atlas registry
│       └── items/
│           └── *.png          — 16×16 weapon textures
└── behavior_pack/
    ├── manifest.json          — Pack metadata with RP dependency
    ├── pack_icon.png
    ├── items/
    │   └── *.json             — Item component definitions
    └── recipes/
        └── *.json             — Crafting recipe definitions (if any recipes saved)
```

Each item JSON uses the [Minecraft Bedrock 1.20 item format](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/itemreference/) and includes components like `minecraft:damage`, `minecraft:durability`, `minecraft:cooldown`, and optionally `minecraft:repairable`.

---

## 🛠️ Tech Stack

| Library | Purpose |
|---------|---------|
| [Fabric.js 5.3](https://fabricjs.com) | Canvas pixel art editor |
| [iro.js 5](https://iro.js.org) | Color picker |
| [JSZip 3.10](https://stuk.github.io/jszip/) | ZIP / `.mcaddon` generation |
| [FileSaver.js 2](https://github.com/eligrey/FileSaver.js) | File download trigger |
| [Phosphor Icons](https://phosphoricons.com) | UI icons |

All libraries loaded from CDN. No build step required.

---

*This is a fun app made for my kids with the help of AI. It isn't a serious project, but it IS seriously cool.*
