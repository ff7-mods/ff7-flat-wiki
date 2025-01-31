---
title: Attack_data
---

## KERNEL.BIN - Section 2: Attack data format

*(Note: Akari and NFITC1 have some minor differences with respect to information on this page. Most of this page comes from NFITC1's work on WallMarket)* This section contains the data for the different attacks. Each record is 28 bytes long.

| Offset | Length | Description |
|----|----|----|
| 0x00 | 1 byte | Attack % |
| 0x01 | 1 byte | [Impact Effect Id](Battle/Impact_Effect_Id_List) |
| 0x02 | 1 byte | Target Hurt Action Index |
| 0x03 | 1 byte | Unknown |
| 0x04 | 2 byte | Casting cost |
| 0x06 | 2 bytes | [Impact Sound](Battle/Sound_Effect_Id_List) |
| 0x08 | 2 bytes | [Camera Movement Id](Battle/Camera_Movement_Id_List?redlink=1) for single target. |
| 0x0A | 2 bytes | [Camera Movement Id](Battle/Camera_Movement_Id_List?redlink=1) for multiple targets. |
| 0x0C | 1 byte | [Target Flags](Battle/Targeting_Data) |
| 0x0D | 1 byte | [Attack Effect Id](Battle/Attack_Effect_Id_List) |
| 0x0E | 1 byte | [Damage Calculation](Battle/Damage_Calculation) |
| 0x0F | 1 byte | Strength of attack for damage calculation |
| 0x10 | 1 byte | Condition sub-menu |
|  | 00 | Party HP |
|  | 01 | Party MP |
|  | 02 | Party Status |
|  | Other | None |
| 0x11 | 1 byte | Status Effect Change |
|  | 3Fh | Chance to Inflict/Heal status (out of 63) |
|  | 40h | Cure if inflicted |
|  | 80h | Cure if inflicted, Inflict if not |
| 0x12 | 1 byte | [Attack Additional Effects](Battle/Attack_Special_Effects) |
| 0x13 | 1 byte | Additional Effects Modifier |
| 0x14 | 4 bytes | [Status](Battle/Status_Effects) |
| 0x18 | 2 bytes | [Element](Battle/Elemental_Data) |
| 0x1A | 2 bytes | [Special Attack Flags](Battle/Special_Attack_Flags) |
