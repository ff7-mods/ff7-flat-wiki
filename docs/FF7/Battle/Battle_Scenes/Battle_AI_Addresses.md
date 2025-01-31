---
title: Battle_AI_Addresses
---

*In this page, an "actor" is defined as an entity instance in a battle (scene). The "current actor" is an actor that is executing a script or performing an action. An "active actor" is one that can perform actions. An "action" is defined as an event with a visual representation in battle (eg. an attack or a position change).*

Most of the complexities of AI scripts use different memory addresses to make decisions based on the actor performing an action or the target of an action. There are three categories of address each spanning a separate useable<sup>1</sup> address ranges.

| Range | Usage |
|----|----|
| 0x0000 - 0x03FF | Random Access Variables. No initial value or significance to battle. |
| 0x2000 - 0x21DF | Globally accessible values. Values are the same for all actors. |
| 0x4000 - 0x433F | Actor specific values. Contains information such as HP, MP, Level, stats, etc. One for each Actor, 10 in all. |

Each address references a specific bit of memory rather than a byte which means individual bits can be manipulated without using BIT-wise operations in script. Every 8 address values is the beginning of a byte (ie. 0x0000, 0x0008, etc.). The code used to access an address determines whether a bit, byte, word, or dword is being read/written.  
Addresses must be accessed directly. There is no pointer support to these values accessible in AI scripts.  

## Random Access Variables

These values are used between scripts and not automatically set/cleared at any time during battle. If an address is set to a specific value in one script, it will retain that value when the next script begins. The initial value is 0. Each actor is allotted 1 kilobyte with which to store values and addresses are unique to the actor. Going beyond 3FFh as an address will result in memory leaks.

## Global Values

Generally these contain information about the battle itself. These values are the same when any actor accesses them, although they do change to reflect the battle's events.

| Address | Value |  |
|----|----|----|
| 0x2000 | Command Index of last action performed |  |
| 0x2008 | Action Index of last action performed |  |
| 0x2010 | Memory 1/2 Bank access value |  |
| 0x2018 | DUMMY. Used in one script in a test enemy. |  |
| 0x2020 | Battle Formation (side, pincer, pre-emptive, etc.) |  |
| 0x2038 | Limit Level. Only used by Vincent during transformation. |  |
| 0x2050 | Active Actor List. A bit mask of all active (scripts enabled) actors. |  |
| 0x2060 | Single bit indicating which actor owns the script that is currently executing. Changes as scripts are triggered. |  |
| 0x2070 | Bit mask of actors indicating targets of the current action. Should be set prior to any action. |  |
| 0x2080 | Bit mask of actors indicating actors the current actor considers as allies. Changes as scripts are triggered. |  |
| 0x2090 | Bit mask of *active* actors indicating actors the current actor considers as allies. Changes as scripts are triggered. |  |
| 0x20A0 | Bit mask of actors indicating actors the current actor considers as enemies. Changes as scripts are triggered. |  |
| 0x20B0 | Bit mask of *active* actors indicating actors the current actor considers as enemies. Changes as scripts are triggered. |  |
| 0x20C0 | Bit mask of active player's characters |  |
| 0x20E0 | Bit mask of all active and inactive actors present in the battle. |  |
| 0x2110 | Set of flags indicating battle rewards (some functions unknown; most won't be set until end of battle). |  |
|  | 0x2111 | End battle; Marked as Escaped |
|  | 0x2112 | End battle; Pose for Victory (if 0x2116 is unset) |
|  | 0x2113 | End battle; No Reward |
|  | 0x2114 | End battle (unsets 0x2113 unless escaped, unsets 0x2111 in that case) |
|  | 0x2115 | (unsets 0x2112) |
|  | 0x2116 | No Victory Pose (unsets 0x2115) |
| 0x2120 | Elements of last performed action. |  |
| 0x2140 | Formation Index of the current battle. |  |
| 0x2150 | Index of last performed action. |  |
| 0x2160 | Some sort of flags (unknown effect). |  |
|  | 0x2160 |  |
|  | 0x2161 | Don't apply poison/regen? |
|  | 0x2162 | Other battles in sequence |
|  | 0x2163 | Empty all players' Limit Bars (and other things) |
|  | 0x2164 | Players can learn limits (never unset?) |
|  | 0x2165 | No reward screen? |
| 0x2170 | [Special Attack Flags](../Special_Attack_Flags). |  |
| 0x2180 | Unknown (divisor of some sort related to limits) |  |
| 0x21A0 | During Emerald Weapon battle, keeps track of how many eyes are active. (Possible use in other battles, too) |  |
| 0x21C0 | Party's Gil |  |

## Actor Specific

These values are reflections of a given actor's status. They include some obvious things like Statuses, Level, HP, MP, etc and a few abstract things like Animation IDs for reactions. Every actor has their own copy of these values that reflects their instance. These values are accessed by masking the address with a specific actor(s) in the script. Using the mask will let the script interpreter know which set of physical addresses to use.

| Address | Value |  |
|----|----|----|
| 0x4000 | Bitmask of current [Statuses](../Status_Effects) |  |
| 0x4020 | Set of flags relating to situation. |  |
|  | 0x4020 |  |
|  | 0x4021 | Ally of current actor |
|  | 0x4022 |  |
|  | 0x4023 |  |
|  | 0x4024 |  |
|  | 0x4025 | Defending |
|  | 0x4026 | Back row |
|  | 0x4027 | Attack connects |
|  | 0x4028 | Immune to physical damage |
|  | 0x4029 | Immune to magical damage |
|  | 0x402A |  |
|  | 0x402B | Was covered / Defers damage |
|  | 0x402C | Immune to Death |
|  | 0x402D | Actor is dead |
|  | 0x402E | Actor is invisible |
| 0x4040 | Actor Index |  |
| 0x4048 | Level |  |
| 0x4058 | Greatest Elemental Damage modifier (No damage, half, normal, etc.) |  |
| 0x4060 | Character ID (+10h) for playable Characters, Instance for enemies |  |
| 0x4068 | Physical Attack Power |  |
| 0x4070 | Magic Attack Power |  |
| 0x4078 | Physical Evade |  |
| 0x4080 | Idle Animation ID |  |
| 0x4088 | Damaged Animation ID |  |
| 0x4090 | Back Damage Multiplier |  |
| 0x4098 | Model Size (default is 16) |  |
| 0x40A0 | Dexterity |  |
| 0x40A8 | Luck |  |
| 0x40B0 | Related to Idle Animations |  |
| 0x40B8 | Character that was just covered. (Character index +10h) |  |
| 0x40C0 | Target(s) of last action performed by actor |  |
| 0x40D0 | Previous Attacker |  |
| 0x40E0 | Previous Physical Attacker |  |
| 0x40F0 | Previous Magical Attacker |  |
| 0x4100 | Physical Defense Rating |  |
| 0x4110 | Magical Defense Rating |  |
| 0x4120 | Index of actor |  |
| 0x4130 | Absorbed Elements |  |
| 0x4140 | Current MP |  |
| 0x4150 | Max MP |  |
| 0x4160 | Current HP |  |
| 0x4180 | Max HP |  |
| 0x41A0 | Unknown (Used by Schizo's heads to tell the other head that it is dead. Maybe elsewhere?) |  |
| 0x4220 | Initial Statuses |  |
| 0x4268 | Magic Evade |  |
| 0x4270 | Row |  |
| 0x4278 | Unknown (something to do with the camera?) |  |
| 0x4280 | Gil stolen (Enemies only) |  |
| 0x4290 | Item stolen (Enemies only) |  |
| 0x42A0 | Nullified Elements? |  |
| 0x42B0 | AP actor is worth |  |
| 0x42C0 | Gil actor is worth |  |
| 0x42E0 | EXP actor is worth |  |

  

Thanks to unchecked memory leaks<sup>1</sup>, any actor can directly access another actor's script values. The following table is to be read across to show what address should be used to access another actor's values starting at 4000. For example, Actor 2 can use 4D00 to access Actor6's values. Also, Actor 8 can use 2540 to access Actor 1's values.

| Actors<sup>2</sup> | Actor 0 | Actor 1 | Actor 2 | Actor 3 | Actor 4 | Actor 5 | Actor 6 | Actor 7 | Actor 8 | Actor 9 | RAVs<sup>3</sup> |
|----|----|----|----|----|----|----|----|----|----|----|----|
| Actor 0 | \* | 4340 | 4680 | 49C0 | 4D00 | 5040 | 5380 | 56C0 | 5A00 | 5D40 | 6080 |
| Actor 1 | 2220 | \* | 4340 | 4680 | 49C0 | 4D00 | 5040 | 5380 | 56C0 | 5A00 | 5D40 |
| Actor 2 | 2220 | 2540 | \* | 4340 | 4680 | 49C0 | 4D00 | 5040 | 5380 | 56C0 | 5A00 |
| Actor 3 | 2220 | 2540 | 2880 | \* | 4340 | 4680 | 49C0 | 4D00 | 5040 | 5380 | 56C0 |
| Actor 4 | 2220 | 2540 | 2880 | 2BC0 | \* | 4340 | 4680 | 49C0 | 4D00 | 5040 | 5380 |
| Actor 5 | 2220 | 2540 | 2880 | 2BC0 | 2F00 | \* | 4340 | 4680 | 49C0 | 4D00 | 5040 |
| Actor 6 | 2220 | 2540 | 2880 | 2BC0 | 2F00 | 3240 | \* | 4340 | 4680 | 49C0 | 4D00 |
| Actor 7 | 2220 | 2540 | 2880 | 2BC0 | 2F00 | 3240 | 3580 | \* | 4340 | 4680 | 49C0 |
| Actor 8 | 2220 | 2540 | 2880 | 2BC0 | 2F00 | 3240 | 3580 | 38C0 | \* | 4340 | 4680 |
| Actor 9 | 2220 | 2540 | 2880 | 2BC0 | 2F00 | 3240 | 3580 | 38C0 | 3C00 | \* | 4340 |

This is mostly unhelpful as formations can vary greatly and actors can still indirectly access each other's values based on controllable conditions. There are lots of examples of indirect access, the memory leak trick is just interesting.

  

NOTES:  
1 - Address values are only checked by the minimum value and stored accordingly. The structure in memory stores the Global Variables first, the Actor Variables second, and the Random Access Variables last. Technically, a value of 0xFFFF could be used as an address, but that would result in a memory leak producing erratic results.  
2 - Actors 0-2 are player controlled characters, Actors 4-9 are enemies. Actor 3 is a omnipresent battle actor that holds formation AI, if it exists and is the placeholder for any summon models. It does nothing on its own and is only used in a few boss battles.  
3 - This will access the Random Access Variables starting at 0x0000. This is stupid as it requires more work to get to them. Don't do it this way!  
