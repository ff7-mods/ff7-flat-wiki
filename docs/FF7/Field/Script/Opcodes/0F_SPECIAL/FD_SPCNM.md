---
title: FD_SPCNM
---

- Opcode: **0x0FFD**
- Short name: **SPECIAL: SPCNM**
- Long name: Special: Change Character Name

#### Memory layout

| 0x0F | 0xFD | *M* | *T* |
|------|------|-----|-----|

- **const UByte** *M*: Model ID of character.
- **const UByte** *T*: Text ID of text.

#### Description

This needs to be tested to confirm. This changes the name of a character.
