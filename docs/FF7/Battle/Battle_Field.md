---
title: Battle_Field
---

Battle fields are simple 3d models drawed in 3d space.

They stored in directories STAGE1 and STAGE2. There are lzs archives that unpacked and loaded in PSX space 0x801590e4. Size of unpacked field must be less than 0x8d04. It consist from few concatenated files. First one is settings for field. Last one is texture. All others are meshes.

### Settings (first file)

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Offset</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Size</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Value</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><p>0</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Type of 3d mesh. There are 6 type of meshes:<br />
0 - mesh with horisontal scrolling parts (field 47 - Corel Train Battle).<br />
1 - normal static mesh.<br />
2 - mesh with vertical scrolling parts (field 12 - Shinra Elevators).<br />
3 - mesh with lifestream (field 4e - Final Battle - Sephiroth).<br />
4 - mesh with rotating parts (field 39 - Safer Battle)<br />
5 - normal static mesh, same as 1. (field 01,44,45 - Bizarro Battles)</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>1</p></td>
<td style="text-align: center; background: rgb(255,255,204);"><p>7 bytes</p></td>
<td style="text-align: center; background: rgb(255,255,204);"><p>unknown</p></td>
</tr>
</tbody>
</table>
