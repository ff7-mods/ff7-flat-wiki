---
title: Damage_Calculation
---

In Attacks, Items, and Weapons there exists a single byte that tells the Battle Engine how to calculate damage based on an attack's set Power and the characters stats. Physical and Magical will rely on the caster's "Attack" and "Magic Attack" stat respectively to calculate base damage. This byte is divided into two nybbles (four bits). Upper Nybble determines what considerations are made in calculating damage such as physical/magical, allowing criticals, how to calculate accuracy, etc. There are also three sets of known formulae that are paired with the Upper nybble values. These are selected in the Lower Nybble and determine how to calculate pre-defense damage. Actual calculation includes a random variance (\[3841..4096\] / 4096), a reduction based on a target's "Defense" or "Magic Defense" stats, and other status-related modifications depending on the type of damage. These will also trigger Physical and Magical Counter Attacks respectively. For more details, these can be considered Base Damage Modifiers as described in Terence Fergusson's [Battle Mechanics FAQ](http://www.gamefaqs.com/console/psx/file/197341/22395). *This [more accurate damage formula page](https://wiki.ffrtt.ru/index.php/DamageFormula) contains more detailed information.*

<table>
<thead>
<tr>
<th><p>Upper Value</p></th>
<th><p>Considerations</p></th>
<th><p>Lower Value</p></th>
<th><p>Formula [Damage = ]</p></th>
<th><p>Sadness Check</p></th>
<th><p>Split Damage</p></th>
<th><p>Barrier Check</p></th>
<th><p>Variance</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0X</p></td>
<td><p>Physical, 100% hit rate</p></td>
<td><p>X0</p></td>
<td><p>No Damage calculation</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
</tr>
<tr>
<td><p>1X</p></td>
<td><p>Physical, Use PAccuracy, Allow Critical</p></td>
<td><p>X1</p></td>
<td><p>(Power / 16) * (Stat + [(Level + Stat) / 32] * [(Level * Stat) / 32])</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr>
<td><p>2X</p></td>
<td><p>Magical, Use MAccuracy</p></td>
<td><p>X2</p></td>
<td><p>(Power / 16) * ((Lvl + Stat) * 6)</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr>
<td><p>3X</p></td>
<td><p>Physical, 100% hit rate</p></td>
<td><p>X3</p></td>
<td><p>HP * (Power / 32)</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
</tr>
<tr>
<td><p>4X</p></td>
<td><p>Magical, 100% hit rate</p></td>
<td><p>X4</p></td>
<td><p>MHP * (Power / 32)</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
</tr>
<tr>
<td><p>5X</p></td>
<td><p>Magical, 100% hit rate</p></td>
<td><p>X5</p></td>
<td><p>(Power * 22) + ((Level + Stat) * 6)</p></td>
<td><p><br />
</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
<td><p>Yes</p></td>
</tr>
<tr>
<td><p>8X</p></td>
<td><p>Magical, Hit chance MOD target level = hit</p></td>
<td><p>X6</p></td>
<td><p>Power * 20</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
</tr>
<tr>
<td><p>9X</p></td>
<td><p>Magical, "Manipulate" accuracy</p></td>
<td><p>X7</p></td>
<td><p>Power / 32</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p>Yes</p></td>
</tr>
<tr>
<td><p>BX</p></td>
<td><p>Physical, use PAccuracy</p></td>
<td><p>X8</p></td>
<td><p>Recovery</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
</tr>
<tr>
<td colspan="2" rowspan="2" style="text-align: center; background: rgb(204,204,255);"></td>
<td><p>X9</p></td>
<td><p>Throw</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
</tr>
<tr>
<td><p>XA</p></td>
<td><p>Coin</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
<td><p><br />
</p></td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p>6X</p></td>
<td><p>Physical, Use PAccuracy, Allow Critical, Special Formulae</p></td>
<td><p>X0</p></td>
<td><p>100% User's HP</p></td>
<td colspan="4" rowspan="18" style="text-align: center; background: rgb(204,204,255);"></td>
</tr>
<tr>
<td><p>7X</p></td>
<td><p>Magical, Use MAccuracy, Special Formulae</p></td>
<td><p>X1</p></td>
<td><p>User's MHP - HP</p></td>
</tr>
<tr>
<td colspan="2" rowspan="6" style="text-align: center; background: rgb(204,204,255);"></td>
<td><p>X8</p></td>
<td><p>Dice Roll<sup>[NOTE]</sup> x 100</p></td>
</tr>
<tr>
<td><p>X9</p></td>
<td><p>Number of Escapes * 256</p></td>
</tr>
<tr>
<td><p>XA</p></td>
<td><p>Target's HP - 1</p></td>
</tr>
<tr>
<td><p>XB</p></td>
<td><p>Number of hours on game clock * 100 + number of minutes in game clock</p></td>
</tr>
<tr>
<td><p>XC</p></td>
<td><p>10 x Target's Kills</p></td>
</tr>
<tr>
<td><p>XD</p></td>
<td><p>1111 x Target's Materia</p></td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p>AX</p></td>
<td><p>Same as 11h, but allow alterations to the final damage or power of attack</p></td>
<td><p>X0</p></td>
<td><p>Damage * (1 + [User's Status Effects <sup>See NOTE</sup>])</p></td>
</tr>
<tr>
<td colspan="2" rowspan="8" style="text-align: center; background: rgb(204,204,255);"></td>
<td><p>X1</p></td>
<td><p>Damage * (2 if Near-Death, 4 if in D.Sentence [can stack to 8], 1 if neither)</p></td>
</tr>
<tr>
<td><p>X2</p></td>
<td><p>Damage * (1 + Dead Allies)</p></td>
</tr>
<tr>
<td><p>X3</p></td>
<td><p>Power becomes average of all Targets' Levels</p></td>
</tr>
<tr>
<td><p>X4</p></td>
<td><p>Power becomes 1 + ( ( Power * 3 * HP ) / MHP )</p></td>
</tr>
<tr>
<td><p>X5</p></td>
<td><p>Power becomes 1 + ( ( Power * 3 * MP ) / MMP )</p></td>
</tr>
<tr>
<td><p>X6</p></td>
<td><p>Power becomes 1 + ( Power * [AP on Weapon <sup>See NOTE</sup> / 10000] / 16 )</p></td>
</tr>
<tr>
<td><p>X7</p></td>
<td><p>Power becomes 10 + ( [Character's Kills / 128] * Power) / 16 )</p></td>
</tr>
<tr>
<td><p>X8</p></td>
<td><p>Power becomes 1 + ( [Limit Level * Limit Units / 16] * Power ) / 16</p></td>
</tr>
</tbody>
</table>

NOTES: For the X8 special formula, the game will "grant" between two and six dice based on level (one additional for every ten levels above 20, max 6). The values of each of these dice will be added and then multiplied by the greatest number of repeating values (not the number of occurrences of the highest value). Ex: The values 2, 3, 5, 5, 2, 2 come up. The values are added (19) then, since there are three twos, it is multiplied by three. For A0 damage multiplier, the multiplier is increased by one for the following effects on the user:

- Near-death
- Poison
- Sadness
- Silence
- Slow
- Darkness

and increased by two for the following:

- D.Sentence
- Slow-numb

For A6 multiplier, Mastered Materia will use the highest level of AP they can hold. ex. When Knights of Round is mastered, its AP is set to 16,777,215 in the materia menu. Since KoR's level 5 AP requirement is 500,000 only 500,000 will be considered in the total.

Any damage formula on an attack can still set status, but standard damage formula 0X will not apply any visual changes due to effects.

Ex. Midgar Zolom's "Change" attack is damage type 00h, but gets set to poison him when he uses it. He will not glow green until he is targeted by another command that is not damage type 00h.
