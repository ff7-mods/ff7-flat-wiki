---
title: 72_BTLMD
---

- Opcode: **0x72**
- Short name: **BTLMD**
- Long name: Battle Mode

#### Memory layout

| 0x72 | *B* |
|------|-----|

#### Arguments

- **const UShort** *B*: Bit field representing battle modes.

#### Description

Sets properties for the battle module. The argument is a bit field with bits that can be ORd together to set multiple battle properties.

#### Bit Tables

All the bytes used by the game are listed here, along with some that are not used but still have an effect on the battle module. The purpose of the bits not listed in the tables is not yet known, but they likely affect the battle module in an as-yet unseen way.

##### First Byte (MSB)

<table>
<thead>
<tr>
<th style="background:rgb(204,204,204)"><p>Bit</p></th>
<th style="background:rgb(204,204,204)"><p>Description (Bit set to 1)</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0x80 (10000000)</p></td>
<td><p>Do not display the AP/EXP/Gil/items received screens.</p></td>
</tr>
<tr>
<td><p>0x40 (01000000)</p></td>
<td><p>Activates the battle arena. The next chosen <a href="70_BATTLE" title="wikilink">BATTLE</a> instead takes place in the arena,<br />
but keeping the same enemy formation. The "keep going/no way" interface is enabled.</p></td>
</tr>
<tr>
<td><p>0x20 (00100000)</p></td>
<td><p>Do not play the battle victory music.</p></td>
</tr>
<tr>
<td><p>0x08 (00001000)</p></td>
<td><p>The party cannot escape the battle.</p></td>
</tr>
<tr>
<td><p>0x04 (00000100)</p></td>
<td><p>Pre-emptive attack.</p></td>
</tr>
<tr>
<td><p>0x02 (00000010)</p></td>
<td><p>The battle is timed; the player must complete the battle before the timer reaches zero,<br />
or the battle exits, with no AP/EXP/Gil/items received screens displayed.</p></td>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</tbody>
</table>

##### Second Byte

| Bit | Description (Bit set to 1) |
|----|----|
| 0x01 (00000001) | Disable game over. After a party defeat, the game returns to the previous field. |
|  |  |
