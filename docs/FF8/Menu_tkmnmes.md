---
title: Menu_tkmnmes
---

These files have a good deal of the Menu text.

### Header

<table><thead><tr class="header"><th><p>Type</p></th><th><p>Size</p></th><th><p>Value</p></th><th><p>Description</p></th></tr></thead><tbody><tr class="odd"><td><p>UInt16</p></td><td><p>2</p></td><td><p>Pad_Count</p></td><td><p>Always <strong>16</strong></p></td></tr><tr class="even"><td><p>UInt16[Pad_Count]</p></td><td><p>2 * Pad_count</p></td><td><p>Paddings</p></td><td><p>The padding value leads to start of string offsets Can be <strong>0x00</strong> ignore those<br />
First one is usually <strong>0x36</strong></p></td></tr></tbody></table>

### String Offsets

| Type                    | Size               | Value         | Description                                                               |
|-------------------------|--------------------|---------------|---------------------------------------------------------------------------|
| UInt16                  | 2                  | Offset\_Count | Number of offsets before strings start                                    |
| UInt16\[Offset\_Count\] | 2 \* Offset\_count | Offsets       | The offset value points to start of a string Can be **0x00** ignore those |

### String

Strings end with **0x00**. [Strings are encoded](String_Encoding.md).  
**\[Start of string location\]** = **\[Start of file\]** + **\[Padding value\]** + **\[String offset value\]**
