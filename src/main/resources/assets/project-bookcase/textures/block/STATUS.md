# Texture Status

## Approach

Data-driven: block model JSON references vanilla textures directly via the `minecraft:`
namespace. Only the book-spine face of the regular bookshelf needs a custom PNG per wood
type — **12 files total**.

All other faces (chiseled bookshelf sides, top, empty front, occupied front) reference
vanilla textures in the model JSON and require no image assets from this mod.

## Pixel layout

Rows 0–1 and 14–15 are plank strips (recolored per wood type).
Rows 2–13 are book spines (identical across all variants — do not change).

See TEXTURES.md for the full spec and extraction instructions.
Each `<wood>_bookshelf.txt` contains the exact hex palette and visual description for
that wood type.

## Progress

| Wood       | PNG ready |
|------------|-----------|
| oak        | [ ]       |
| spruce     | [ ]       |
| birch      | [ ]       |
| jungle     | [ ]       |
| acacia     | [ ]       |
| dark_oak   | [ ]       |
| mangrove   | [ ]       |
| cherry     | [ ]       |
| pale_oak   | [ ]       |
| crimson    | [ ]       |
| warped     | [ ]       |
| bamboo     | [ ]       |

Check the box and delete the corresponding `.txt` when a PNG is committed.