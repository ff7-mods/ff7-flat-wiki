---
title: Weapon data
---

[Home](Main%20Page.md) > [FF7](FF7.md) > Weapon data

## KERNEL.BIN - Section 6: Weapon data format

This section contains the weapon data. Each weapon attribute is 44 bytes
long.

|           Offset            | Length                                     | Description                                                                                                 |
|:---------------------------:|--------------------------------------------|-------------------------------------------------------------------------------------------------------------|
|            0x00             | 1 byte                                     | [Target Flags][]                                                                                            |
|            0x01             | 1 byte                                     | [Attack Effect Id][]. Always 0xFF. Isn't used for weapon in game.                                           |
|            0x02             | 1 byte                                     | [Damage Calculation][]                                                                                      |
|            0x03             | 1 byte                                     | Not used. Always 0xFF.                                                                                      |
|            0x04             | 1 byte                                     | Weapon attack strength for damage formula.                                                                  |
|            0x05             | 1 byte                                     | [Status Attack][]. This is index of status bit.                                                             |
|            0x06             | 1 byte                                     | Materia growth rate (0, 1, 2, 3 for None, Normal, Double, Triple. All other values are "Normal" Growth)     |
|            0x07             | 1 byte                                     | Critical hit chance (%)                                                                                     |
|            0x08             | 1 byte                                     | Weapon hit chance (%)                                                                                       |
|            0x09             | 1 byte                                     | Weapon model                                                                                                |
|                             | Upper nybble                               | Attack animation modifier (For Barret and Vincent only)                                                     |
|        Lower nybble         | Weapon model index                         |                                                                                                             |
|            0x0A             | 1 byte                                     | Alignment. Always 0xFF.                                                                                     |
|            0x0B             | 1 byte                                     | Mask for access high sound id (0x100+).                                                                     |
|            0x0C             | 2 bytes                                    | [Camera Movement Id][]. Used for both single and multiple targeted attacks with this weapon. Always 0xFFFF. |
|            0x0E             | 2 bytes                                    | Equip Mask                                                                                                  |
|                             | 0x0001                                     | Equipable on Cloud                                                                                          |
|           0x0002            | Equipable on Barret                        |                                                                                                             |
|           0x0004            | Equipable on Tifa                          |                                                                                                             |
|           0x0008            | Equipable on Aeris                         |                                                                                                             |
|           0x0010            | Equipable on Red XIII                      |                                                                                                             |
|           0x0020            | Equipable on Yuffie                        |                                                                                                             |
|           0x0040            | Equipable on Cait Sith                     |                                                                                                             |
|           0x0080            | Equipable on Vincent                       |                                                                                                             |
|           0x0100            | Equipable on Cid                           |                                                                                                             |
|           0x0200            | Equipable on Young Cloud                   |                                                                                                             |
|           0x0400            | Equipable on Sephiroth                     |                                                                                                             |
|            0x10             | 2 bytes                                    | [Attack Element][]                                                                                          |
|            0x12             | 2 bytes                                    | Unknown \[Always 0xFFFF\]                                                                                   |
|            0x14             | 4 bytes                                    | Increase Stat Type                                                                                          |
|                             | 0xFF                                       | None                                                                                                        |
|            0x00             | Strength                                   |                                                                                                             |
|            0x01             | Vitality                                   |                                                                                                             |
|            0x02             | Magic                                      |                                                                                                             |
|            0x03             | Spirit                                     |                                                                                                             |
|            0x04             | Dexterity                                  |                                                                                                             |
|            0x05             | Luck                                       |                                                                                                             |
|            0x18             | 4 bytes                                    | Stat Amount Increased (Based on above)                                                                      |
|            0x1C             | 8 bytes                                    | Materia Slots                                                                                               |
|                             | 0x00                                       | No Slot                                                                                                     |
|            0x01             | Empty Unlinked Slot (no growth-equips)     |                                                                                                             |
|            0x02             | Empty Left Linked Slot (no growth-equips)  |                                                                                                             |
|            0x03             | Empty Right Linked Slot (no growth-equips) |                                                                                                             |
|            0x05             | Unlinked Slot                              |                                                                                                             |
|            0x06             | Left Linked Slot                           |                                                                                                             |
|            0x07             | Right Linked Slot                          |                                                                                                             |
|            0x24             | 1 bytes                                    | [Sound Effect Id][] for normal hit.                                                                         |
|            0x25             | 1 bytes                                    | [Sound Effect Id][] for critical hit.                                                                       |
|            0x26             | 1 bytes                                    | [Sound Effect Id][] for missed attack.                                                                      |
|            0x27             | 1 byte                                     | [Impact Effect Id][]                                                                                        |
|            0x28             | 2 bytes                                    | [Special Attack Flags][]. Always 0xFFFF.                                                                    |
|            0x2A             | 2 bytes                                    | Restriction Mask (If the following bits are 0)                                                              |
|                             | 01h                                        | Can be sold                                                                                                 |
|             02h             | Can be used in Battle                      |                                                                                                             |
|             04h             | Can be used in Menu Out of Battle          |                                                                                                             |
| Other values have no effect |                                            |                                                                                                             |

  [Target Flags]: FF7/Battle/Targeting%20Data.md "wikilink"
  [Attack Effect Id]: FF7/Battle/Attack%20Effect%20Id%20List.md "wikilink"
  [Damage Calculation]: FF7/Battle/Damage%20Calculation.md "wikilink"
  [Status Attack]: FF7/Battle/Status%20Effects.md "wikilink"
  [Camera Movement Id]: FF7/Battle/Camera%20Movement%20Id%20List.md "wikilink"
  [Attack Element]: FF7/Battle/Elemental%20Data.md "wikilink"
  [Sound Effect Id]: FF7/Battle/Sound%20Effect%20Id%20List.md "wikilink"
  [Impact Effect Id]: FF7/Battle/Impact%20Effect%20Id%20List.md "wikilink"
  [Special Attack Flags]: FF7/Battle/Special%20Attack%20Flags.md "wikilink"
