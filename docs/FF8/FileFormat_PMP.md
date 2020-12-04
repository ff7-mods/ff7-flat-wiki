---
title: FileFormat_PMP
---

By myst6re.

## Particle Data

When this file is empty, it is only 4 bytes = `0x20202020`. Else:

| Offset | Size      | Data        |
|--------|-----------|-------------|
| 0      | 2 bytes   | Unknown     |
| 2      | 2 bytes   | Unknown     |
| 4      | 512 bytes | 16 palettes |
| 516    | *Varies*  | Image Data  |

### Palettes

16 palettes of 16 colors in native PSX format (R5G5B5 with one mask bit).

### Image Data

The actual image data can be read as a single 256 pixels wide image, the height depends on the size of the data (`height = dataSize / 128`).
