---
title: FileFormat_ONE
---

By myst6re.

# chara.one Archive

Each field contains a chara.one file that contains multiple field models (PNJs), or calls to main fields models (Squall, Laguna...).

## Header

| Offset               | Length                           | Description                                   |
|----------------------|----------------------------------|-----------------------------------------------|
| 0x00                 | 4 bytes                          | Number of models (not present in ps version!) |
| 0x04                 | nbModels \* varies bytes         | Model headers                                 |
| 0x04 + nbModels\*var | 256-(0x04 + nbModels\*var) bytes | Padding (the header is always 256 bytes)      |

### Model header

For each model:

| Offset        | Length  | Description                                                                                                                     |
|---------------|---------|---------------------------------------------------------------------------------------------------------------------------------|
| 0x00          | 4 bytes | Offset to model textures + data. Warning: in pc version, you must add 4 to this offset!                                         |
| 0x04          | 4 bytes | Size of model data                                                                                                              |
| 0x08          | 4 bytes | Size of model data (bis). Warning: Sometimes not present!                                                                       |
| 0x0C          | 4 bytes | if this DWORD &gt;&gt; 24 == 0xd0, there is no tim offset list, and "model data offset" is 0 because this is a main field model |
| 0x10          | Varies  | Tim offset (relative to the "Offset to model textures + data") list, ends with value 0xFFFFFFFF                                 |
| 0x10 + Varies | 4 bytes | Model data offset (relative to the "Offset to model textures + data")                                                           |
| 0x14 + Varies | 8 bytes | Model name, usefull when you must call a main field model                                                                       |
| 0x1C + Varies | 4 bytes | Always 0XEEEEEEEE                                                                                                               |

## Data

This is the same data structure as a [MCH model](FF8/FileFormat_MCH "wikilink") (without header). In the PlayStation version, each model textures + data is [LZS](../FF7/LZS_format.md) compressed.
