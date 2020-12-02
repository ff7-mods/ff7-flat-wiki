---
title: Item data
---

[Home](/Main%20Page.md) > [FF7](/FF7.md) > Item data

## KERNEL.BIN - Section 5: Item data format

This section contains the item data. Each item record is 28 bytes long.

| Offset | Length                            | Description                                                   |
|:------:|-----------------------------------|---------------------------------------------------------------|
|  0x00  | 8 bytes                           | Unknown                                                       |
|  0x08  | 2 bytes                           | [Camera Movement Id][] for single and multiple target attack. |
|  0x0A  | 2 bytes                           | Restriction Mask (If the following bits are 0)                |
|        | 01h                               | Can be sold                                                   |
|  02h   | Can be used in Battle             |                                                               |
|  04h   | Can be used in Menu Out of Battle |                                                               |
|  0x0C  | 1 byte                            | [Target Flags][]                                              |
|  0x0D  | 1 byte                            | [Attack Effect Id][]                                          |
|  0x0E  | 1 byte                            | [Damage Calculation][]                                        |
|  0x0F  | 1 byte                            | Item power for damage calculation.                            |
|  0x10  | 1 byte                            | Condition sub-menu                                            |
|        | 00                                | Party HP                                                      |
|   01   | Party MP                          |                                                               |
|   02   | Party Status                      |                                                               |
| Other  | None                              |                                                               |
|  0x11  | 1 byte                            | Status Effect Change                                          |
|        | 3Fh                               | Chance to Inflict/Heal status (out of 63)                     |
|  40h   | Cure if inflicted                 |                                                               |
|  80h   | Cure if inflicted, Inflict if not |                                                               |
|  0x12  | 1 byte                            | [Attack Additional Effects][]                                 |
|  0x13  | 1 byte                            | Additional Effects Modifier                                   |
|  0x14  | 4 bytes                           | [Status Effects][]                                            |
|  0x18  | 2 bytes                           | [Attack Element][]                                            |
|  0x1A  | 2 bytes                           | [Special Attack Flags][]                                      |

  [Camera Movement Id]: /FF7/Battle/Camera%20Movement%20Id%20List.md "wikilink"
  [Target Flags]: /FF7/Battle/Targeting%20Data.md "wikilink"
  [Attack Effect Id]: /FF7/Battle/Attack%20Effect%20Id%20List.md "wikilink"
  [Damage Calculation]: /FF7/Battle/Damage%20Calculation.md "wikilink"
  [Attack Additional Effects]: /FF7/Battle/Attack%20Special%20Effects.md
    "wikilink"
  [Status Effects]: /FF7/Battle/Status%20Effects.md "wikilink"
  [Attack Element]: /FF7/Battle/Elemental%20Data.md "wikilink"
  [Special Attack Flags]: /FF7/Battle/Special%20Attack%20Flags.md "wikilink"
