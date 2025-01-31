---
title: D3_SLINE
---

- Opcode: **0xD3**
- Short name: **SLINE**
- Long name: Set Line

#### Memory layout

| 0xD3 | *B1 / B2* | *B3 / B4* | *B5 / B6* | *XA* | *YA* | *ZA* | *XB* | *YB* | *ZB* |
|------|-----------|-----------|-----------|------|------|------|------|------|------|

#### Arguments

- **const Bit\[4\]** *B1*: Bank for *XA*, or zero if *XA* is specified as a literal value.
- **const Bit\[4\]** *B2*: Bank for *YA*, or zero if *YA* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank for *ZA*, or zero if *ZA* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank for *XB*, or zero if *XB* is specified as a literal value.
- **const Bit\[4\]** *B5*: Bank for *YB*, or zero if *YB* is specified as a literal value.
- **const Bit\[4\]** *B6*: Bank for *ZB*, or zero if *ZB* is specified as a literal value.
- **const Short** *XA*: X-coordinate of the first point of the line, or address to find value if *B1* is non-zero.
- **const Short** *YA*: Y-coordinate of the first point of the line, or address to find value if *B2* is non-zero.
- **const Short** *ZA*: Z-coordinate of the first point of the line, or address to find value if *B3* is non-zero.
- **const Short** *XB*: X-coordinate of the second point of the line, or address to find value if *B4* is non-zero.
- **const Short** *YB*: Y-coordinate of the second point of the line, or address to find value if *B5* is non-zero.
- **const Short** *ZB*: Z-coordinate of the second point of the line, or address to find value if *B6* is non-zero.

#### Description

Alters the two points of a previously defined [LINE](D0_LINE). In addition to allowing a line to be adjusted after creation, this opcode also provides the ability to retrieve line end-point values from memory.

If two or more lines are defined in one entity, SLINE only updates the first LINE definition.
