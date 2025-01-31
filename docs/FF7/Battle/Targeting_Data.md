---
title: Targeting_Data
---

## Targeting Data

Before targeting is explained in full, some information of rows must be understood. There are two or three rows in any battle. Most normal battles have two rows, allies and enemies. Pincer Attacks and Side Attacks have three rows. Two enemy rows for pincer attacks and one for side attacks. Furthermore, under most conditions, a "viable target" is a battle participant (enemy or ally) that is not inflicted with "Death".

Targeting is set by a single byte with eight different effects for each bit that is set:

<table>
<thead>
<tr>
<th><p>Bit</p></th>
<th><p>Effect on Target Selection</p></th>
<th><p>Explanation</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>01h</p></td>
<td><p>Enable Selection</p></td>
<td><p>Cursor will move to the battle field and a target can be selected with the constraints in the following.</p></td>
</tr>
<tr>
<td><p>02h</p></td>
<td><p>Start Cursor on Enemy Row</p></td>
<td><p>Cursor will start on the first enemy row.</p></td>
</tr>
<tr>
<td><p>04h</p></td>
<td><p>Multiple Targets by Default</p></td>
<td><p>Cursor will select all targets in a given row.</p></td>
</tr>
<tr>
<td><p>08h</p></td>
<td><p>Toggle Multiple/Single Targets</p></td>
<td><p>Caster can switch cursor between multiple targets or single targets. (Also indicates if damage will be split among targets)</p></td>
</tr>
<tr>
<td><p>10h</p></td>
<td><p>One Row Only</p></td>
<td><p>Cursor will only target allies or enemies as defined in 02h and cannot be moved from the row.</p></td>
</tr>
<tr>
<td><p>20h<br />
</p></td>
<td><p>"Short Range"<br />
(physical damage only)</p></td>
<td><ul>
<li>If the target or the caster is not in the front of their row, the target will take half damage.</li>
<li>For every attack this is enabled, they are constrained by the <a href="Battle_Scenes#Binary_.22Cover_Flags.22" title="wikilink">Binary "Cover Flags"</a></li>
</ul></td>
</tr>
<tr>
<td><p>40h</p></td>
<td><p>All Rows</p></td>
<td><p>Cursor will select viable targets</p></td>
</tr>
<tr>
<td><p>80h</p></td>
<td><p>Random Target among Selected</p></td>
<td><p>When multiple targets are selected, one will be selected at random to be the receiving target. Cursor will cycle among all viable targets.</p></td>
</tr>
</tbody>
</table>

Targets are set in three places. On Commands, on Attacks, and on Weapons. The Command's target (if not NULL \[FFh\]) trumps any target information provided by the Attack or the Weapon. As such, it is analyzed first. Any additional settings are added through the weapon or attack.  
This is further trumped by "Confuse" and "Berserk" which will set the target data to C0h and 97h respectively. Confuse will pick any available command to perform and Berserk will just attack with the equipped weapon.

Although the cursor can move to an ally with the "Death" status, if no targets selected to receive the attack are viable the attack will "re-target". A dead enemy cannot be targeted, dead allies can. This is true for monsters and PCs. A "re-target" takes the original targeting data and multiple targets and random is added.

Eg1: Fire (Target of 0Fh) is selected to be performed on an enemy. That action is put into the queue, but the enemy dies before Fire is performed. Fire's targeting data (0Fh) is then and'd with 87h.

`New Target = (0Fh And 87h) = 87h ' random enemy`

Eg2: Cure (Target of 0Dh) is queued to heal a suffering ally. Before Cure is cast, the ally dies. Cure is re-targeted:

`New Target = (0Dh And 87h) = 85h ' random ally`

NOTE: Setting a target in enemy attack data does not control how the enemy selects targets. That is defined in their AI. Targets in enemy attack data only get used while they are being manipulated.

## Examples:

Defend/Change: Has a target of 00h. This will only allow the caster to perform the command on itself.

Shield: This has a target of 01h. This will only allow the caster to perform the spell on itself or one ally.

Summons: Target of 17h. A PC cannot perform a summon that attacks on his/her own character or row. It will only target all of any enemy row, but only one row.

Some of Aeris's and Cait Sith's Limit Breaks: Set at 15h. Same as above, but only the caster's row.

Most weapons: 23h. This makes some of the weapons into a short range attack. If the "Long Range" Materia is equipped, bit 20h of this targeting data is forced to 0.

Comet2/Berserk: 97h. This will target one target of the enemy row at random.

Roulette: C7h. Will choose one target at random from among all battle participants not inflicted with "Death" status.
