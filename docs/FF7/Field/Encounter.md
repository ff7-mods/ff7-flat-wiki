---
title: Encounter
---

## Overview

The encounter section provides encounter data for the field by referencing [battle IDs](../Battle/Battle_Scenes) and providing probabilites for each type of encounter required. The section consists of two *encounter tables* that hold sets of these battle configurations; these tables may be switched between using field scripting. The two encounter tables are contiguous and follow directly after the section's length description; due to the presence of the two encounter tables regardless of whether they are used or not, the section length is always 48 bytes.

` struct SECTION_ENCOUNTER`  
` {`  
`     u32       section_length;    /* 0x30 */`  
`     ENC_TABLE tables[2];`  
` };`

  

## Encounter Table Structure

` struct ENC_TABLE`  
` {`  
`     u8        enabled;`  
`     u8        rate;`  
`     ENCOUNTER enc_standard[6];`  
`     ENCOUNTER enc_special[4];`  
`     u16       _pad;`  
` }`

The first byte of the table provides a switch to signify whether this table is used or not. If set to *0* encounters will not be used, regardless of the table contents; *1* signifies the table will be used. The second byte signifies the main encounter rate, and ranges from 0xFF (battles occur infrequently) to 0x01 (battles occur very frequently). 0x00 value causes a division by zero.

Following these are the ten encounter structures; these are divided into two groups of six and four, as detailed below. There is also a further two-byte "padding" value, used for alignment.

### Switching Between Tables

The purpose of two tables is to allow the scripting system to switch between a choice of two sets of encounter data. This is used in-game to allow two levels of difficulty within one field, so that if the player revisits an area in a later part of the game (such as areas of Midgar), the enemies will be suitably more difficult. This can be implemented by placing "easier" encounters in the first table, harder encounter IDs in the second table, and switching appropriately (perhaps by checking the Plot Point Variable).

Tables are switched between by simply passing a 0 or 1 to the [BTLTB](Script/Opcodes/4B_BTLTB) opcode, representing the required table. The first table is the default if no BTLTB opcode is specified; either table may be empty, but if switched to using BTLTB, encounters will be deactivated as there will be no encounter data set for that table.

## Encounter Structure

` struct ENCOUNTER                      /* pseudo */`  
` {`  
`     bit       prob[6];`  
`     bit       encounter_id[10];`  
` }`

` // Create from two-byte value`  
` u16 enc_entry;                        /* holds the read value */`  
` u8  prob         = enc_entry >> 10;`  
` u16 encounter_id = enc_entry & 0x03FF;`

Each individual two-byte encounter entry is further split into two groups of bits.

The first six bits denote the probability for this encounter; the sum of all the probabilites for the standard encounters is 64, though this is not the case for the special battles. For further information on how encounter probabilities are used and calculated, Terence Fergusson's [Battle Mechanics Guide](http://db.gamefaqs.com/console/psx/file/final_fantasy_vii_enemy_mech.txt) contains detailed information.

The second ten bits denote the [ID](../Battle/Battle_Scenes) of the battle.

### Encounter Entry Types

The set of ten battles is split into two groups. The first six battles are generic battles, intended for general use, whose probabilities must total 64. The final four battles are intended to be used in the following order:

- Back Attack 1
- Back Attack 2
- Side Attack
- Attack From Both Sides
