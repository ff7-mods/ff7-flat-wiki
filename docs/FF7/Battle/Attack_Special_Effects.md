---
title: Attack_Special_Effects
---

Attacks and Items can have additional Special Effects that take place after Damage Calculation is performed. Several of them take a Modifier that further defines what action to take. If the Effect doesn't take a modifier, the modifier is NULL (FFh). In addition, these effects have specific timings. There are six different timings that will be explained later. Here are the valid values (between 0 - 23h) with examples of some attacks that have these values. If another value is provided it will be ignored. [Damage Calculations](Damage_Calculation) A0 - A8 are handled using the highlighted effects and defaulting to damage calculation 11h.

<table>
<thead>
<tr>
<th><p>Value</p></th>
<th><p>Effect</p></th>
<th><p>Attacks with this Property</p></th>
<th><p>T0</p></th>
<th><p>T1</p></th>
<th><p>T2</p></th>
<th><p>T3</p></th>
<th><p>T4</p></th>
<th><p>T5</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>00</p></td>
<td><p>Multiple [Modifier] hits</p></td>
<td><p>Comet2, Ultimate End, Several Limit Attacks (Omnislash, Catastrophe, etc)</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>01</p></td>
<td><p>If all enemies are immune to statuses attempted to inflict, perform Gunge Lance</p></td>
<td><p>Steel Bladed Sword</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>02</p></td>
<td><p>Randomly summon Fat-Chocobo if [Modifier] &gt; [0..255]</p></td>
<td><p>DeathBlow</p></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>03</p></td>
<td><p>Caster's Main Script takes control and become [Modifier]</p></td>
<td><p>Vincent's Limit Breaks</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>04</p></td>
<td><p>Cause back-attack damage to target in row [Modifier] (Physical damage calculations only)</p></td>
<td><p>Aps' Tsunami (there are two of these)</p></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>05</p></td>
<td><p>End battle, no reward</p></td>
<td><p>Escape</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>06</p></td>
<td><p>Steal (Level * 20) Gil from target (No affect on players' attacks)</p></td>
<td><p>Bandit's "Hold Up"</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>07</p></td>
<td><p>Steal Item from target (No affect on players' attacks)</p></td>
<td><p>Bandit's "Mug"</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>08</p></td>
<td><p>Randomly select one of the next six animation indexes to display</p></td>
<td><p>Cait Sith's Slot: Toy Box</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>09</p></td>
<td><p>If Attacker's level = Target's level, Damage = Damage * 8</p></td>
<td><p>Goblin Punch</p></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>0A</p></td>
<td style="background: rgb(255,255,204)"><p>Damage multiplied based on attacker's statuses</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A0 (Master Fist)</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>0B</p></td>
<td style="background: rgb(255,255,204)"><p>Multiplier starts at 1<br />
If attacker at or below 1/4 HP, Multiplier *2<br />
If attacker inflicted with Death Sentence, Multiplier *4 [can stack for total of *8]<br />
Damage multiplied by Multiplier</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A1 (Powersoul)</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>0C</p></td>
<td style="background: rgb(255,255,204)"><p>Damage multiplied by 1 + number of KO'd allies</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A2 (Princess Guard)</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>0D</p></td>
<td style="background: rgb(255,255,204)"><p>Attack power becomes average of targets' levels</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A3 (Conformer)</p></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>0E</p></td>
<td><p>Resurrect Dead Allies</p></td>
<td><p>Rebirth Flame</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>0F</p></td>
<td><p>Bring up Slot Wheel</p></td>
<td><p>Cait Sith's "Slot" Limit Break <sup>NOTE</sup></p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>10</p></td>
<td><p>Removes other allies from battle and gives their stats to caster</p></td>
<td><p>Cait Sith's Slot: Transform</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>11</p></td>
<td><p>Removes target from battle and flags as if "Death" (No effect on enemies)</p></td>
<td><p>Ruby Weapon's "Whirlsand"; Ghost Ship's "Goannai"; Carry Armor's Arms' "Arm Grab"</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>12</p></td>
<td><p>Removes target from battle and flags as escaped (No effect on enemies)</p></td>
<td><p>Midgar Zolom's "Blown Away"</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>13</p></td>
<td><p>Perform Critical Hit based on result of slot</p></td>
<td><p>Tifa's Limit Breaks <sup>NOTE</sup></p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>14</p></td>
<td><p>Fills limit gauge of other allies (If an enemy uses this it will fill all players' bars)</p></td>
<td><p>Aeris's Limit Break: "Fury Brand"</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>15</p></td>
<td><p>Alters Targets' physical and magic damage and defense by [Modifier-100]% (Stackable)</p></td>
<td><p>Hero Drink</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>16</p></td>
<td><p>Alter Performer's Evasion by [Modifier - 100]% per target (Stackable)<sup>NOTE</sup></p></td>
<td><p>Red XIII's Limit Break: Lunatic High</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>17</p></td>
<td><p>Alter Performer's Attack by [Modifier - 100]% per target (Stackable)<sup>NOTE</sup></p></td>
<td><p>Red XIII's Limit Break: Howling Moon</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>18</p></td>
<td><p>Perform Attack/Item [Modifier] upon completion<sup>NOTE</sup></p></td>
<td><p>Vincent's Limit Break: "Satan Slam"; Cloud's Limit Break: "Finishing Touch"</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>19</p></td>
<td><p>All Targets' Rows are changed (will not work on enemies)</p></td>
<td><p>Hell Rider V2's "Electromag"</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>1A</p></td>
<td><p>Perform attack [Modifier] on other row members</p></td>
<td><p>Blade Beam</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>1B</p></td>
<td><p>Removes Caster from battle and flags as escaped (will not work on Allies)</p></td>
<td><p>Various Enemies' "Escape"</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>1C</p></td>
<td><p>Alter Targets' Defenses by [Modifier - 100]% (Stackable)</p></td>
<td><p>Dragon Force</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>1D</p></td>
<td><p>Returns Target from Escaped status</p></td>
<td><p>Carry Armor's Arms' &lt;unnamed&gt;</p></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>1E</p></td>
<td style="background: rgb(255,255,204)"><p>Attack's power becomes 1 + ( ( Power * 3 * HP ) / MHP )</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A4 (Ultima Weapon, HP Shout)</p></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>1F</p></td>
<td style="background: rgb(255,255,204)"><p>Attack's power becomes 1 + ( ( Power * 3 * MP ) / MMP )</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A5 (Limited Moon, Venus Gospel)</p></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>20</p></td>
<td style="background: rgb(255,255,204)"><p>Attack's power becomes 1 + ( Power * (AP on weapon / 10000) / 16 )</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A6 (Missing Score)</p></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>21</p></td>
<td style="background: rgb(255,255,204)"><p>Attack's power becomes 10 + ( [Character's Kills / 128] * Power) / 16 )</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A7 (Death Penalty)</p></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>22</p></td>
<td style="background: rgb(255,255,204)"><p>Attack's power becomes 1 + ( ( [Limit Level * Limit Units / 16] * Power ) / 16 )</p></td>
<td style="background: rgb(255,255,204)"><p>Damage Calculation A8 (Premium Heart)</p></td>
<td style="background: rgb(255,255,204)"><p>X</p></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
<td style="background: rgb(255,255,204)"></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>23</p></td>
<td><p>Receive no Gil or items from enemy hit by this attack (No effect on Allies)</p></td>
<td><p>Remove</p></td>
<td></td>
<td></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td></td>
</tr>
</tbody>
</table>

  
NOTE: For these two Effects, if they are not called as part of a Limit Break they will return an index of 0.  
For Effect 0Fh, this means performing "Game Over" and ending the battle in a victory.  
For Effect 13h, the player's characters' battle queues freeze and no PC can perform any action after this was selected. Enemies still attack. The reason for this is unknown.  
For Effects 16h and 17h, only the performer gets the stat boost. The in-game English description of Lunatic High suggests this is not intentional. The statuses are granted by the actual Limit attack. Since Howling Moon only targets the caster this isn't an issue, but additional targets would not get the stat boost.  
For Effect 18h, the game assumes the second attack's animation indexes are of the same scope as the first attack's (e.g. if you call an enemy skill as the follow up for a spell, the game will (attempt) to use a magic animation).

## Timings

As mentioned, the different timings indicate when the effects take place during the process of executing the command:

- **T0:** Takes place immediately before damage calculation occurs. If there is no damage calculation, this will not activate.
- **T1:** Takes place immediately after damage calculation occurs. If there is no damage calculation, this will not activate.
- **T2:** After Command is selected and loaded, but before anything actually happens.
- **T3:** Takes place immediately after damage calculation would occur. Will activate whether there is damage done or not.
- **T4:** Activates as long as the action passes accuracy checks (Doesn't 'Miss').
- **T5:** Action Resolution. After Damage Calculations are done this will be triggered for each active actor.

For effects that have more than one timing, there are more than one functions associated with them.  
ex.  
Effect 05h ends the battle without reward. It has a T2 and a T5 command. The T2 command will check if the battle can be escaped from. If it can it sets the "run modifier" to full. The T5 command will actually set the battle to having been escaped from. If it's possible to escape from the battle, it will.
