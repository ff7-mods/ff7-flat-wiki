---
title: FileFormat TDW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > FileFormat TDW

By myst6re.

## font

For the field, this is a file for the japanese PSX version only, it adds
text characters. In the PC version, the file *sysfnt.tdw* in main.fs is
used to know the width of each character, the texture part is not used
(you can find the used texture in sysfnt.tex in menu.fs).

| Offset       | Size                      | Data                        |
|--------------|---------------------------|-----------------------------|
| 0            | 4 bytes                   | Offset to widths (always 8) |
| 4            | 4 bytes                   | Offset to data              |
| offsetWidths | offsetData - offsetWidths | [Character widths][]        |
| offsetData   | varies                    | [Texture (TIM)][]           |

### Character widths

Each width is 4 bits (two widths per byte).

### Texture

Texture is a [TIM file][] with 8 colors: dark grey, grey, yellow, red,
green, blue, purple and white.

*TODO: Explain the palette mechanism in japanese version (16 pal instead
of 8).*

  [Character widths]: #user-content-character-widths "wikilink"
  [Texture (TIM)]: #user-content-texture "wikilink"
  [TIM file]: /ff7-flat-wiki/PSX/TIM%20format.md "wikilink"
