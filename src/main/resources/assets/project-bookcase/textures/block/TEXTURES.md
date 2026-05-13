# Texture Design Guide

Vanilla source textures are in the Minecraft jar:
`~/Library/Application Support/minecraft/versions/26.1.2/26.1.2.jar`

Extract them with:
```bash
cd ~/Library/Application\ Support/minecraft/versions/26.1.2
unzip 26.1.2.jar "assets/minecraft/textures/block/bookshelf.png" \
                  "assets/minecraft/textures/block/chiseled_bookshelf_*.png" \
                  -d /tmp/mc-textures
open /tmp/mc-textures/assets/minecraft/textures/block/
```

---

## Specs

- **Size:** 16×16 px
- **Format:** PNG, no transparency (fully opaque)
- **Color depth:** 8-bit or 32-bit RGBA both fine — Minecraft ignores the alpha channel on solid block faces

---

## Files to Create

For each of the 12 wood types, replace the `.txt` placeholder with a real `.png`:

| File | Base it on | What to change |
|------|-----------|----------------|
| `<wood>_bookshelf.png` | `bookshelf.png` | Swap the plank strips to match the wood type's color/grain |
| `<wood>_chiseled_bookshelf_empty.png` | `chiseled_bookshelf_empty.png` | Swap plank border color |
| `<wood>_chiseled_bookshelf_occupied.png` | `chiseled_bookshelf_occupied.png` | Swap plank border color |
| `<wood>_chiseled_bookshelf_side.png` | `chiseled_bookshelf_side.png` | Replace with the wood type's plank texture |
| `<wood>_chiseled_bookshelf_top.png` | `chiseled_bookshelf_top.png` | Replace with the wood type's plank texture |

Wood types: `oak`, `spruce`, `birch`, `jungle`, `acacia`, `dark_oak`, `mangrove`, `cherry`, `pale_oak`, `crimson`, `warped`, `bamboo`

---

## Tips

- The side and top textures for the chiseled bookshelf are essentially just the wood's plank texture — you can copy `<wood>_planks.png` straight from the jar as a starting point.
- The book-spine face (`_bookshelf.png`) has the plank strips at the top and bottom edges; only those strips need recoloring per wood type.
- The empty/occupied faces have a thin plank border — recolor just that border strip.
- Use the vanilla `<wood>_planks.png` textures (also in the jar) as color reference for each type.

---

## When Done

Delete the corresponding `.txt` placeholder and commit the `.png` in its place.
