---
title: 0xfd
---

## 0xFD (Unknown Yet)

Has two 8-bit parameters.

Unknown Opcode.

Parameters writes to Global Configuration structure (I think :)) at 0x8009A104.

1st parameter offset: 0x5a

2nd parameter offset: 0x56

In structure this two parameters are 16-bit.

Opcode also clears two another 16-bit numbers at offsets 0x58 and 0x5c.

All 4 parameters mentioned are checked in every iteration of opcode processing (this needs more investigation).
