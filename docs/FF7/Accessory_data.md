---
title: Accessory_data
---

## KERNEL.BIN - Section 8: Accessory data format

This section contains the accessory data. Each record is 16 bytes long.

| Offset | Length | Description |  |
|:--:|----|----|----|
| 0x00 | 2 bytes | Stat Bonus |  |
|   |  | 0xFF | None |
|  |  | 0x00 | Strength |
|  |  | 0x01 | Vitality |
|  |  | 0x02 | Magic |
|  |  | 0x03 | Spirit |
|  |  | 0x04 | Dexterity |
|  |  | 0x05 | Luck |
| 0x02 | 2 bytes | Bonus Amount |  |
| 0x04 | 1 byte | Elemental Strength |  |
|   |  | 0x00 | Absorb |
|  |  | 0x01 | Nullify |
|  |  | 0x02 | Halve |
| 0x05 | 1 byte | Special Effect |  |
|   |  | 0xFF | None |
|  |  | 0x00 | Haste |
|  |  | 0x01 | Berserk |
|  |  | 0x02 | Curse Ring |
|  |  | 0x03 | Reflect |
|  |  | 0x04 | Increase Stealing Rate |
|  |  | 0x05 | Increase Manipulation Rate |
|  |  | 0x06 | Barrier / MBarrier |
|  |  |  |  |
| 0x06 | 2 bytes | [Elements Affected](Battle/Elemental_Data) |  |
| 0x08 | 4 bytes | [Status Protect](Battle/Status_Effects) |  |
| 0x0C | 2 bytes | Equip Mask |  |
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
| 0x0E | 2 bytes | Restriction Mask (If the following bits are 0) |  |
|   |  | 01h | Can be sold |
|  |  | 02h | Can be used in Battle |
|  |  | 04h | Can be used in Menu Out of Battle |
|  |  | Other values have no effect |  |
