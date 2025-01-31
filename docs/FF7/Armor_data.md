---
title: Armor_data
---

## KERNEL.BIN - Section 7: Armor data format

This section contains the armor data. Each record is 36 bytes long.

| Offset | Length | Description |  |
|:--:|----|----|----|
| 0x00 | 1 byte | Unknown |  |
| 0x01 | 1 byte | Damage Type, Based off values of Elemental Type |  |
|   |  | 0xFF | Normal |
|  |  | 0x00 | Absorb |
|  |  | 0x01 | Nullify |
|  |  | 0x02 | Halve |
| 0x02 | 1 byte | Defense |  |
| 0x03 | 1 byte | Magic Defense |  |
| 0x04 | 1 byte | Defense % |  |
| 0x05 | 1 byte | Magic Defense % |  |
| 0x06 | 1 byte | [Status Defense](Battle/Status_Effects). Index of status bit. |  |
| 0x07 | 2 bytes | Unknown |  |
| 0x09 | 8 bytes | Materia Slots |  |
|   |  | 0x00 | No Slot |
|  |  | 0x01 | Empty Unlinked Slot |
|  |  | 0x02 | Empty Left Linked Slot |
|  |  | 0x03 | Empty Right linked Slot |
|  |  | 0x05 | Unlinked Slot |
|  |  | 0x06 | Left Linked Slot |
|  |  | 0x07 | Right Linked Slot |
| 0x11 | 1 byte | Materia Growth (0, 1, 2, 3 for None, Normal, Double, Triple. All other values are "Normal" Growth) |  |
| 0x12 | 2 bytes | Equip Mask |  |
|   |  | 0x0001 | Equipable on Cloud |
|  |  | 0x0002 | Equipable on Barret |
|  |  | 0x0004 | Equipable on Tifa |
|  |  | 0x0008 | Equipable on Aeris |
|  |  | 0x0010 | Equipable on Red XIII |
|  |  | 0x0020 | Equipable on Yuffie |
|  |  | 0x0040 | Equipable on Cait Sith |
|  |  | 0x0080 | Equipable on Vincent |
|  |  | 0x0100 | Equipable on Cid |
|  |  | 0x0200 | Equipable on Young Cloud |
|  |  | 0x0400 | Equipable on Sephiroth |
| 0x14 | 2 bytes | [Elemental Defense](Battle/Elemental_Data) |  |
| 0x16 | 2 bytes | Unknown \[Always 0x00FF\] |  |
| 0x18 | 4 bytes | Stat Bonus |  |
|   |  | 0xFF | None |
|  |  | 0x00 | Strength |
|  |  | 0x01 | Vitality |
|  |  | 0x02 | Magic |
|  |  | 0x03 | Spirit |
|  |  | 0x04 | Dexterity |
|  |  | 0x05 | Luck |
| 0x1C | 4 bytes | Stat Increase |  |
| 0x20 | 2 bytes | Restriction Mask (If the following bits are 0) |  |
|   |  | 01h | Can be sold |
|  |  | 02h | Can be used in Battle |
|  |  | 04h | Can be used in Menu Out of Battle |
|  |  | Other values have no effect |  |
| 0x22 | 2 bytes | Unknown \[Always 0xFFFF\] |  |
