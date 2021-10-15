---
title: FileFormat_MSK
---

By myst6re.

## Mask Files?

| Offset | Size              | Data           |
|--------|-------------------|----------------|
| 0      | 4 bytes           | Count          |
| 4      | 24 \* Count bytes | Mask position? |

I think for "Count" frame, there are four points (4 \* 6 bytes = 4 \* (x,y,z)) in space.

Additional info by Kaspar03:

In every sector of every .msk files there are:

-4 starting bytes that may be always different (and for a yet unknown reason for the same field they're not the same in every release of the game... my best guess is that they could be offsets to data stored in a file that may not always be the same size eg. ff8.exe)

-16 middle bytes that are always identical (67 02 20 2D 0C 00 00 00 0C 00 00 00 9C 43 C7 63)

-4 ending bytes that may differ from file to file but that are always the same within the same msk.

Even if the purpose of these files is still unknown because of this repeated content it's quite unlikely these files can contain 3D model data or animation data.

Edit:

in PC version of the game all msk files the last 20 bytes of each sector are always the same: 44 A2 C6 20 90 CA 31 00 0C 00 00 00 90 CA 31 00 24 8A F4 66

in remaster version of the game all msk files the last 20 bytes of each sector are always the same: 2B 21 01 94 88 CC 34 00 0C 00 00 00 88 CC 34 00 24 8A 53 66
