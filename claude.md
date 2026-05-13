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

### Approach

Block models reference vanilla textures directly via the `minecraft:` namespace. The only
custom texture per wood type is the **book-spine face** of the regular bookshelf — 12 files total.

| Face | Source |
|------|--------|
| Regular bookshelf sides | `project-bookcase:block/<wood>_bookshelf` (custom PNG) |
| Regular bookshelf top/bottom | `minecraft:block/<wood>_planks` (vanilla) |
| Chiseled bookshelf sides | `minecraft:block/<wood>_planks` (vanilla) |
| Chiseled bookshelf top/bottom | `minecraft:block/<wood>_planks` (vanilla) |
| Chiseled bookshelf front (empty) | `minecraft:block/chiseled_bookshelf_empty` (vanilla) |
| Chiseled bookshelf front (occupied) | `minecraft:block/chiseled_bookshelf_occupied` (vanilla) |

### Files to create

One PNG per wood type, 12 total:

```
src/main/resources/assets/project-bookcase/textures/block/<wood>_bookshelf.png
```

Base each on vanilla's `bookshelf.png` — only the plank strips at the top and bottom
edges need recoloring to match the wood type. Use `<wood>_planks.png` from the jar as
color reference.

Placeholder `.txt` files exist for all 12. Replace each with the real `.png` when ready.