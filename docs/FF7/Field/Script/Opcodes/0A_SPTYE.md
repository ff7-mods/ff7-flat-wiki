---
title: 0A_SPTYE
---

- Opcode: **0x0A**
- Short name: **SPTYE**
- Long name: Set Party From Memory

#### Memory layout

| 0x0A | *B1 / B2* | *B3 / 0* | *A1* | *A2* | *A3* |
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

Sets the current party, using the [Character ID](../../Character_ID) values found at the banks and addresses specified by the arguments. It is possible to retrieve from three different banks.

This is used to set a party back to the player's configuration after a certain event, that requires specific characters that have been set using [PRTYE](CA_PRTYE), has completed. An example would be the party being set to Barret only for the Dyne event/battle, and then returning the party back to the player's configuration before the Dyne event occurs.
