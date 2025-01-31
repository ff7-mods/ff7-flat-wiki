---
title: Item_data
---

## KERNEL.BIN - Section 5: Item data format

This section contains the item data. Each item record is 28 bytes long.

| Offset | Length | Description |  |
|:--:|----|----|----|
| 0x00 | 8 bytes | Unknown | Always 0xFFFFFFFF |
| 0x08 | 2 bytes | [Camera Movement Id](Battle/Camera_Movement_Id_List) for single and multiple target attack. |  |
| 0x0A | 2 bytes | Restriction Mask (If the following bits are 0) |  |
|   |  | 01h | Can be sold |
|  |  | 02h | Can be used in Battle |
|  |  | 04h | Can be used in Menu Out of Battle |
| 0x0C | 1 byte | [Target Flags](Battle/Targeting_Data) |  |
| 0x0D | 1 byte | [Attack Effect Id](Battle/Attack_Effect_Id_List) |  |
| 0x0E | 1 byte | [Damage Calculation](Battle/Damage_Calculation) |  |
| 0x0F | 1 byte | Item power for damage calculation. |  |
| 0x10 | 1 byte | Condition sub-menu |  |
|   |  | 00 | Party HP |
|  |  | 01 | Party MP |
|  |  | 02 | Party Status |
|  |  | Other | None |
| 0x11 | 1 byte | Status Effect Change |  |
|   |  | 3Fh | Chance to Inflict/Heal status (out of 63) |
|  |  | 40h | Cure if inflicted |
|  |  | 80h | Cure if inflicted, Inflict if not |
| 0x12 | 1 byte | [Attack Additional Effects](Battle/Attack_Special_Effects) |  |
| 0x13 | 1 byte | Additional Effects Modifier |  |
| 0x14 | 4 bytes | [Status Effects](Battle/Status_Effects) |  |
| 0x18 | 2 bytes | [Attack Element](Battle/Elemental_Data) |  |
| 0x1A | 2 bytes | [Special Attack Flags](Battle/Special_Attack_Flags) |  |
