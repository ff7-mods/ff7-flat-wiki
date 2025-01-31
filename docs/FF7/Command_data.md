---
title: Command_data
---

## KERNEL.BIN - Section 1: Command data format

This section contains the data for Menu commands.  
There are 32 entries of 8 bytes in the following format:

| Offset | Length | Description |  |
|:--:|----|----|----|
| 0x00 | 1 byte | Initial Cursor Action\* |  |
| 0x01 | 1 byte | [Target Flags](Battle/Targeting_Data) |  |
| 0x02 | 2 bytes | Unknown (Always \[FFFFh\]) |  |
| 0x04 | 2 bytes | [Camera Movement Id](Battle/Camera_Movement_Id_List) for single target. |  |
| 0x06 | 2 bytes | [Camera Movement Id](Battle/Camera_Movement_Id_List) for multiple targets. |  |

  
\*Initial Cursor Action: The different values will tell it what to do or what menu to bring up:

| Value | Effect                             |
|-------|------------------------------------|
| 00h   | Perform command using target data  |
| 01h   | Magic Menu                         |
| 02h   | Summon Menu                        |
| 03h   | Item Menu                          |
| 04h   | E.Skill Menu                       |
| 05h   | Throw Menu                         |
| 06h   | Limit Menu                         |
| 07h   | Enable Target Selection via Cursor |
| 08h   | W-Magic Menu                       |
| 09h   | W-Summon Menu                      |
| 0Ah   | W-Item Menu                        |
| 0Bh   | Coin Menu                          |

The commands themselves are hard-coded into the Battle Engine and their actions cannot be changed via editing the KERNEL.BIN  
Example of what this means: If the summon command was changed to bring up the magic menu and Cure was selected, the battle engine would perform Choco/Mog summon instead. Why? Because The Battle Engine is expecting summon data from command 03h. While the target was considered based on the targeting information of Cure, which has the same magic index as Choco/Mog has summon index, the attack the Battle Engine selected to perform was Summon attack 00h which is Choco/Mog.
