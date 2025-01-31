---
title: Battle_Mechanics
---

This page will be for Battle memory structures. This is consistent with the memory structure of the PC version. PSX may or may not reflect these structures.

## Command Defaults

Each command type has default execution values that can, in some cases, be overridden. These come from a hard-coded structure in the executable.

| Offset | Default            |
|--------|--------------------|
| 0h     | Animation          |
| 1h     | Damage Calculation |
| 2h     | Command Properties |

## Queued Actions

When a command is selected either by a player character or an enemy the action is inserted into a priority queue. Up to 64 actions can be queued. On each update loop, the main Queue function will pop off the next action with the lowest priority and execute it in FIFO order within priority bands.

Queue entries have the following structure in memory:

| Offset | Value |
|----|----|
| 0 | Action Priority (limits/counters 0, player chosen spells 6) |
| 1 | Queue position within priority band |
| 2 | Attacker actor ID |
| 3 | Action command index (e.g CMD_MAGIC = 0x02) |
| 4 | Action attack index (e.g Bolt = 0x21). (This index is absolute, not command relative) |
| 6 | Action target mask |

## AI Structure

There is a single block of memory that holds AI information on the current running script. Each Actor "owns" this while their scripts are executing.

| Offset     | Function                                  |
|------------|-------------------------------------------|
| 0h         | Actor Index                               |
| 4h         | Script Position                           |
| 8h         | Remaining Stack Space (initially 200h)    |
| 0Ch        | Current AI OpCode                         |
| 10h        | OpCode Lower Nybble                       |
| 14h        | OpCode Upper Nybble                       |
| 18h        | First Group Type                          |
| 1Ch        | Second Group Type                         |
| 20h        | OpCode Lower Nybble (related to group 1?) |
| 24h        | OpCode Lower Nybble (related to group 2?) |
| 28h        | Mask of *non-null* values in Group 1      |
| 2Ah        | Mask of *non-null* values in Group 2      |
| 2Ch - 50h  | Group 1 of variables                      |
| 54h - 78h  | Group 2 of variables                      |
| 7Ch - 27Ch | Stack of values                           |

## Active Character Data

This is an array that each playable character maintains an instance of.

| Offset | Value |  |
|----|----|----|
| 000h | Character ID |  |
| 001h | Cover Chance |  |
| 002h | Strength |  |
| 003h | Vitality |  |
| 004h | Magic |  |
| 005h | Spirit |  |
| 006h | Speed |  |
| 007h | Luck |  |
| 008h | Phys Attack |  |
| 00Ah | Phys Def |  |
| 00Ch | Mag Attack |  |
| 00Eh | Mag Def |  |
| 010h | Current HP |  |
| 012h | Max HP |  |
| 014h | Current MP |  |
| 016h | Max MP |  |
| 018h | Timer |  |
| 01Ch | Counter Attack Action Index |  |
| 01Eh | Counter Attack Chance |  |
| 021h | Some sort of divisor? |  |
| 023h | Character Flags (Underwater, Long Range, HP\<-\>MP, etc) |  |
| 024h | Eight entries of three bytes... |  |
| 03Ch | Attacking Elements |  |
| 03Eh | Halved Elements |  |
| 040h | Nullified Elements |  |
| 042h | Absorbed Elements |  |
| 044h | Attacking Elements |  |
| 048h | Immune Statuses |  |
| 04Ch | Enabled Command Menu (16 entries of 6 bytes) |  |
| 0ACh | Limit Actions for current Limit Level |  |
| 0B4h | Enabled Limit Data (three entries in Attack Data format(0x1C)) |  |
| 108h | Enabled Magics (54 entries of 8 bytes) |  |
|  | 0 | Magic Index |
|  | 1h | MP Cost |
|  | 2h | All Count |
|  | 3h | Quad Enabled? |
|  | 4h | Quad Count? |
|  | 5h | Target Data |
|  | 6h | Properties |
| 2C8h | Enabled Summons (format like above) |  |
| 348h | Enabled ESkills (format like above) |  |
| 408h | First 11 bytes of Weapon Data |  |
| 40Dh | Status of weapon added to Attacking Statuses above |  |
| 410h | Weapon's Accuracy |  |
| 418h | Additional Attack Elements |  |
| 41Ch | Four sets of two DWords : (Stat to increase, Increase value) |  |
| 43Ch | Gil Bonus granted by this character |  |
| 43Dh | Encounter rate "" |  |
| 43Eh | Chocobo Chance "" |  |
| 43Fh | PreEmptive Chance "" |  |

## Actor Battle Data

Similar to Active Character Data, but more detailed. This data is dependent on who is performing the current action and only one instance of it exists during each action and all stats are relative to the performing actor and current action unless otherwise noted. Addresses 200h and above will change for each target of the action.

| Offset | Value |  |
|----|----|----|
| 0h | Index |  |
| 4h | Level |  |
| 8h | Formation Entry (Enemy A, Enemy B, etc) |  |
| 0Ch | Command Index |  |
| 10h | Action Index |  |
| 14h | Action Animation Base (for relative to absolute animation indexes) |  |
| 18h | Allowed Targets (Active and targetable) |  |
| 1Ch | Active Allies? |  |
| 20h | Command Animation (player characters only) |  |
| 24h | [Attack Effect](Attack_Effect_Id_List) |  |
| 28h | Command Index (again) |  |
| 2Ch | Action Index (again) |  |
| 30h | Self Mask |  |
| 38h | MP Cost |  |
| 3Ch | Action Accuracy |  |
| 40h | [Damage Calculation](Damage_Calculation) |  |
| 44h | [Action's Element](Elemental_Data) |  |
| 48h | Action's Power |  |
| 4Ch | Phys/Mag Attack Power |  |
| 50h | Action's Target(s) Mask |  |
| 54h | Normal Impact Sound |  |
| 58h | Critical Impact Sound |  |
| 5Ch | Miss Sound |  |
| 60h | Single Target Camera |  |
| 64h | Multi Target Camera |  |
| 68h | Action Reaction Animation Index |  |
| 6Ch | [Attack Special Effects](Attack_Special_Effects) |  |
| 78h | Non-self target mask? |  |
| 80h | [Inflicting Status(es)](Status_Effects) |  |
| 84h | [Curing Status(es)](Status_Effects) |  |
| 88h | [Toggling Status(es)](Status_Effects) |  |
| 8Ch | Chance to inflict Status |  |
| 90h | Command Properties (details pending) |  |
| 94h | Target Mask |  |
| 98h | Attack Index position in scene data (enemy only) |  |
| A0h | Action Accuracy function (upper nybble of [Damage Calculation](Damage_Calculation)) |  |
| A4h | Action Damage function (lower nybble of [Damage Calculation](Damage_Calculation) |  |
| ACh | Quad Magic Count? |  |
| B0h | Number of attack damage calculations? |  |
| B4h | Follow-up action count (Tifa's Limits, Finishing Touch, etc) |  |
| B8h | Number of Targets? |  |
| BCh | [Attack Additional Effects](Attack_Special_Effects) |  |
| C0h | Additional Effect Modifier |  |
| C4h | Attack Power |  |
| C8h | Actor's current status |  |
| D0h - D7h | Follow-up Action(s) |  |
| D8h | Actor's Strength |  |
| DCh | Used during String display? |  |
| E0h | Number of successful hits |  |
| F0h | Character-specific action properties (mp absorb, hp absorb, etc) |  |
| F8h | Related to enabled magic. Also ACh above. |  |
| FCh | Multiple hit count |  |
| 100h - 1FFh | large unused gap |  |
| 200h | ??? |  |
| 204h | Character Map (players only) |  |
| 208h | Current Target Index |  |
| 20Ch | Formation Slot |  |
| 210h | Target's Phys/Mag Def (whichever attack type is) |  |
| 214h | Damage done to target |  |
| 218h | Properties of attack |  |
|  | 1 | missed |
|  | 2 | Physical if set; Magical if unset |
|  | 4 | Attempt Steal |
|  | 20 | Won't Miss |
|  | 4000 | Physical Barrier |
|  | 8000 | Magical Barrier |
|  | 40000 | ??? |
|  | 800000 | ??? |
| 220h | More properties (heal, critical, damage MP, etc) |  |
| 224h | Target's reaction animation |  |
| 228h | Target's status |  |
| 22Ch | Target's status immunities |  |
| 230h | Damage level to current Action |  |
|  | 1 | Death (if not immune) |
|  | 2 | Always hit? |
|  | 4 | Double (Damage & Accuracy) |
|  | 8 | Normal (Never checked) |
|  | 10 | Half (Damage & Accuracy) |
|  | 20 | Null (won't miss?) |
|  | 40 | Absorb (won't miss?) |
|  | 80 | Full-Heal |
| 234h | Target condition flags (back exposed, multiple targets, etc) |  |
| 238h | Status(es) to add to Target |  |
| 23Ch | Status(es) to Cure from Target |  |
| 240h | Status(es) to Toggle from Target |  |
| 244h | All Target's statuses that will be affected from action |  |
| 248h | Sound to play (determined from hit/critical/miss sounds above) |  |
| 24Ch | Action Animation to use (varies from single/multiple targets) |  |
| 254h | Target's Level |  |
| 258h | Target's HP |  |
| 25Ch | Target's MP |  |
| 260h | Action's final Accuracy |  |
