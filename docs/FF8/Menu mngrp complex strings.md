---
title: Menu mngrp complex strings
---

[Home](../Main Page.md) > [FF8](../FF8.md) > Menu mngrp complex strings

## Seek Map

Before the string sections, there is a section with a map of seek data.

### Header

| Type   | Size | Value | Description               |
|--------|------|-------|---------------------------|
| UInt32 | 4    | Count | Number of seek locations. |
|        |      |       |                           |

### Seek Struct

| Type   | Size | Value           | Description                                        |
|--------|------|-----------------|----------------------------------------------------|
| UInt16 | 2    | Seek\_Location  | From beginning of section to start of String Entry |
| UInt16 | 2    | Section\_Number | 0-5                                                |

## String Entry

| Type                     | Size              | Value                                              | Description                                            |
|--------------------------|-------------------|----------------------------------------------------|--------------------------------------------------------|
| Byte\[6\]                | 6                 | UNK                                                | Fist one is **0xFFFFFFFFFFFF**                         |
| UInt16                   | 2                 | Entry\_Length                                      | Length of entry from start.                            |
| Byte \[Entry\_Length-8\] | Entry\_Length - 8 | [Encoded\_Strings](String Encoding.md) | Entry might have more than string, each ends with 0x00 |
