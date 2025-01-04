---
title: Menu_mngrp_complex_strings
---

## Seek Map
Before the several string sections (5), there is a section with a map of seek data.
The seek map is composed of 4 bytes containing the number of seek location, then for each of those seek location, 4 bytes info. So the total size of the seek map is 4 + 4*(Number seek).

### Number seek
| Type   | Size | Value | Description               |
|--------|------|-------|---------------------------|
| UInt32 | 4    | Count | Number of seek locations. |

### Seek location info

| Type   | Size | Value           | Description                                        |
|--------|------|-----------------|----------------------------------------------------|
| UInt16 | 2    | Seek\_Location  | From beginning of section to start of String Entry |
| UInt16 | 2    | Section\_Number | 0-5                                                |

## String Entry
Then each string complex section is composed of the following data:

| Type                     | Size              | Value                                              | Description                                            |
|--------------------------|-------------------|----------------------------------------------------|--------------------------------------------------------|
| Byte\[6\]                | 6                 | UNK                                                | First one is **0xFFFFFFFFFFFF**                        |
| UInt16                   | 2                 | Entry\_Length                                      | Length of entry from start.                            |
| Byte \[Entry\_Length-8\] | Entry\_Length - 8 | [Encoded\_Strings](String_Encoding.md)             | Entry might have more than string, each ends with 0x00 |
