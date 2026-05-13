# project-bookcase

A Fabric mod for Minecraft 26.1.2 that adds bookshelf and chiseled bookshelf variants
for all vanilla wood types. Both block types are fully functional — regular bookshelves
boost enchanting tables, and chiseled bookshelves store books exactly like vanilla.

This mod is used on the prismclt Minecraft server.

---

## Scope

**In scope:**
- Vanilla wood type variants for the regular bookshelf
- Vanilla wood type variants for the chiseled bookshelf
- Full vanilla functionality preserved (enchanting power, book storage)
- Data-driven recipes, loot tables, and blockstates via data generation

**Out of scope (for now):**
- Cross-mod wood compatibility (handled by a future project-bookcase-compat mod)
- Custom wood types (handled by project-lumber)
- Any new gameplay mechanics

---

## Project Structure

```
src/
  client/   # Client-only code (rendering, visuals)
  main/     # Shared code (blocks, items, data gen) — runs on both client and server
```

The client/main split is intentional and important. The chiseled bookshelf has
client-side rendering logic. Never call client-only code from main — it will crash
dedicated servers.

---

## Key Commands

```bash
./gradlew build          # Compile and package the mod JAR
./gradlew runClient      # Launch a test Minecraft client with the mod loaded
./gradlew runServer      # Launch a test dedicated server
./gradlew runDatagen     # Run data generation (produces recipes, loot tables, blockstates)
```

Always run `runDatagen` after adding a new wood variant before building.

---

## Naming Conventions

Block IDs follow the pattern `project-bookcase:<wood_type>_bookshelf` and
`project-bookcase:<wood_type>_chiseled_bookshelf`.

Example: `project-bookcase:spruce_bookshelf`, `project-bookcase:spruce_chiseled_bookshelf`

Java classes follow the same pattern:
- `SpruceBookshelfBlock`
- `SpruceChiseledBookshelfBlock`

---

## Adding a New Wood Variant

1. Register the block in the appropriate registry file in `main/`
2. Add a block item for it
3. Add a data gen provider entry for recipes, loot tables, and blockstates
4. Run `./gradlew runDatagen`
5. Add textures to `src/main/resources/assets/project-bookcase/textures/block/`
6. Verify in-game with `./gradlew runClient`

---

## Architecture Notes

- This mod deliberately has no dependencies beyond Fabric API
- No cross-mod compat is implemented here — that belongs in project-bookcase-compat
- Data generation is the source of truth for recipes and loot tables; do not hand-write
  those JSON files

---

## Textures

### Vanilla texture filenames (from `26.1.2.jar`)

**Regular bookshelf:**
- `bookshelf.png` — the book-spine face (sides); top/bottom reuse `oak_planks.png` from vanilla

**Chiseled bookshelf:**
- `chiseled_bookshelf_empty.png` — front face, all slots empty
- `chiseled_bookshelf_occupied.png` — front face, slots occupied (state-dependent)
- `chiseled_bookshelf_side.png` — side faces (shows wood grain)
- `chiseled_bookshelf_top.png` — top/bottom faces (shows planks)

### Naming pattern for this mod

Prefix vanilla filenames with `<wood_type>_`. Examples:
- `spruce_bookshelf.png`
- `spruce_chiseled_bookshelf_empty.png`
- `spruce_chiseled_bookshelf_side.png`

### Shared vs. unique textures

- **`<wood>_bookshelf.png`** — unique per wood type (book-spine face; plank top/bottom can reference vanilla's `<wood>_planks.png`)
- **`<wood>_chiseled_bookshelf_empty.png`** — the slot pattern is wood-agnostic visually, but a per-wood file is provided for flexibility
- **`<wood>_chiseled_bookshelf_occupied.png`** — same as above
- **`<wood>_chiseled_bookshelf_side.png`** — unique per wood type (wood grain differs)
- **`<wood>_chiseled_bookshelf_top.png`** — unique per wood type (planks pattern differs)

Placeholder `.txt` files exist under `src/main/resources/assets/project-bookcase/textures/block/` for all 12 wood types × 5 textures = 60 files. Replace each `.txt` with the real `.png` when the texture is ready.