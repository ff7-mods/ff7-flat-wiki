---
title: 58_STITM
---

- Opcode: **0x58**
- Short name: **STITM**
- Long name: Set Item

#### Memory layout

| 0x58 | *B1 / B2* | *T* | *A* |
|------|-----------|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Source bank 1, or zero if *T* is set as a constant value.
- **const Bit\[4\]** *B2*: Source bank 2, or zero if *A* is set as a constant value.
- **const UShort** *T*: [Type of item](../Item_ID) to add, or source address to retrieve item type from.
- **const UByte** *A*: Amount of item to add, or source address to retrieve item quantity from.

#### Description

Adds a new item to the inventory. Either the item is added explicitly with values, in which case *B1* and *B2* are zero, or the item type and quantity are retrieved from memory. In this case, bank *B1* and address *T* retrieve the item type, whilst bank *B2* and address *A* retrieve the quantity to add.

#### Example

The following example adds 10 (0xA) Elixirs (ID 0x5) using temporary bank 5 and address 1C for item type, and a value for item quantity.

`SETBYTE(50,1C,5)`  
`STITM(50,1C,0,A)`
