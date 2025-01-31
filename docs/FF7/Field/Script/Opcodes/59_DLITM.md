---
title: 59_DLITM
---

- Opcode: **0x59**
- Short name: **DLITM**
- Long name: Delete Item

#### Memory layout

| 0x59 | *B1 / B2* | *T* | *A* |
|------|-----------|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Source bank 1, or zero if *T* is set as a constant value.
- **const Bit\[4\]** *B2*: Source bank 2, or zero if *A* is set as a constant value.
- **const UShort** *T*: [Type of item](../Item_ID) to delete, or source address to retrieve item type from.
- **const UByte** *A*: Amount of item to remove, or source address to retrieve item quantity from.

#### Description

Removes a quantity of an item from the inventory. Either the item is removed explicitly with values, in which case *B1* and *B2* are zero, or the item type and quantity are retrieved from memory. In this case, bank *B1* and address *T* retrieve the item type, whilst bank *B2* and address *A* retrieve the quantity to remove.
