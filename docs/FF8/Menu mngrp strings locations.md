---
title: Menu mngrp strings locations
---

[Home](Main%20Page.md) > [FF8](FF8.md) > Menu mngrp strings locations

Many strings.

### Header String Offsets

| Type                    | Size               | Value         | Description                                                               |
|-------------------------|--------------------|---------------|---------------------------------------------------------------------------|
| UInt16                  | 2                  | Offset\_Count | Number of offsets before strings start                                    |
| UInt16\[Offset\_Count\] | 2 \* Offset\_count | Offsets       | The offset value points to start of a string Can be **0x00** ignore those |

### String

Strings end with **0x00**. [Strings are encoded][].  
**\[Start of string location\]** = **\[Start of file\]** + **\[String
offset value\]**

  [Strings are encoded]: ../String%20Encoding.md "wikilink"
