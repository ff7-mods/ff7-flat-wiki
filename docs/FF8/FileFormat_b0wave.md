---
title: FileFormat_b0wave
---

By MaKiPL

------------------------------------------------------------------------

b0wave.dat is file containing one 4BPP TIM texture with magic animation sequence, AKAO frame and font data. Current structure:

| Offset | Name                      | Description                             |
|--------|---------------------------|-----------------------------------------|
| 0      | Number of sections        | Number of pointers in file              |
| 4      | Texture offset (4BPP TIM) | Pointer to TIM texture in file (global) |
| 8      | Font Section              | Pointer to Font Section.                |
| 12     | AKAO                      | Pointer to AKAO frame inside file.      |
| 16     | EOF                       | Total size (EOF)                        |

-   Pointers and EOF are **uint32**.

AKAO frame holds "win" music.

## Font Section

Copied from myst6re [.TDW file](FileFormat_TDW.md)

| Offset       | Size                      | Data                                             |
|--------------|---------------------------|--------------------------------------------------|
| 0            | 4 bytes                   | Offset to widths (always 8)                      |
| 4            | 4 bytes                   | Offset to texture                                |
| offsetWidths | offsetData - offsetWidths | [Character widths](#character-widths) |
| offsetData   | varies                    | TIM Texture                                      |

### Character widths

Each width is 4 bits (two widths per byte).
