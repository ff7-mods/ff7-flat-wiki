---
title: 0B_GTPYE
---

- Opcode: **0x0A**
- Short name: **GTPYE**
- Long name: Get Party To Memory

#### Memory layout

| 0x0B | *B1 / B2* | *B3 / 0* | *A1* | *A2* | *A3* |
|------|-----------|----------|------|------|------|

#### Arguments

- **const Bit\[4\]** *B1*: Bank for first party member.
- **const Bit\[4\]** *B2*: Bank for second party member.
- **const Bit\[4\]** *B3*: Bank for third party member.
- **const Bit\[4\]** *0*: Zero.
- **const UByte** *A1*: Address for first party member.
- **const UByte** *A2*: Address for second party member.
- **const UByte** *A3*: Address for third party member.

#### Description

Retrieves the current party's [Character IDs](../../Character_ID) into the banks and addresses specified for each party member. It is possible to retrieve values into three different banks, one for each member.

This is used to store the player's party configuration before they are overridden for a special event that requires a specific character setup. The player's original party configuration can then be set back to its original setup using [SPTYE](0A_SPTYE).
