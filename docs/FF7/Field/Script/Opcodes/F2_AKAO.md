---
title: F2_AKAO
---

- Opcode: **0xF2**
- Short name: **AKAO**
- Long name: Sound Operation (byte param1)

#### Memory layout

| 0xF2 | *B1 / B2* | *B3 / B4* | *0 / B6* | *Op* | *Param1* | *Param2* | *Param3* | *Param4* | *Param5* |
|----|----|----|----|----|----|----|----|----|----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve *Param1*, or zero if *Param1* is specified as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve *Param2*, or zero if *Param2* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve *Param3*, or zero if *Param3* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank to retrieve *Param4*, or zero if *Param4* is specified as a literal value.
- **const Bit\[4\]** *0*: Zero.
- **const Bit\[4\]** *B6*: Bank to retrieve *Param5*, or zero if *Param5* is specified as a literal value.
- **const UByte** *Op*: Operation to perform.
- **const UByte** *Param1*: Parameter 1.
- **const UShort** *Param2*: Parameter 2.
- **const UShort** *Param3*: Parameter 3.
- **const UShort** *Param4*: Parameter 4.
- **const UShort** *Param5*: Parameter 5.

#### Description

Perform an operation described by *Op*, and uses the parameters depending on the operation.

##### Operation list (by [Aali](user:aali "wikilink") and [DLPB](../../../../user:DLPB2)

- **10** Play music \[param1=Music ID\]
- **14** Same as 10
- **15** *Unknown* Serves no significant function
- **18** Play music and resume from last position \[param1=Music ID\]
- **19** Same as 18

------------------------------------------------------------------------

<li>

**20** Play one sound effect \[param1=Panning, param2=Effect ID on channel \#1\]

</li>

<li>

**21** Play two sound effects \[param1=Panning, param2=Effect ID on channel \#1, param3=Effect ID on channel \#2\]

</li>

<li>

**22** Play three sound effects \[param1=Panning, param2=Effect ID on channel \#1, param3=Effect ID on channel \#2, param4=Effect ID on channel \#3\]

</li>

<li>

**23** Play four sound effects \[param1=Panning, param2=Effect ID on channel \#1, param3=Effect ID on channel \#2, param4=Effect ID on channel \#3, param5=Effect ID on channel \#4\]

</li>

<li>

**24** Same as 20

</li>

<li>

**25** Same as 21

</li>

<li>

**26** Same as 22

</li>

<li>

**27** Same as 23

</li>

<li>

**28** Play a sound effect on channel \#1 \[param1=Panning, param2=Effect ID\]

</li>

<li>

**29** Play a sound effect on channel \#2 \[param1=Panning, param2=Effect ID\]

</li>

<li>

**2A** Play a sound effect on channel \#3 \[param1=Panning, param2=Effect ID\]

</li>

<li>

**2B** Play a sound effect on channel \#4 \[param1=Panning, param2=Effect ID\]

</li>

<li>

**30** Play a sound effect on channel \#5 with centre panning

</li>

------------------------------------------------------------------------

<li>

**98** Resumes music and sound effects

</li>

<li>

**99** Pauses music and sound effects

</li>

<li>

**9A** Resumes only the music

</li>

<li>

**9B** Pauses only the music

</li>

<li>

**9C** Resumes only sound effects

</li>

<li>

**9D** Pauses only sound effects

</li>

------------------------------------------------------------------------

<li>

**A0** Volume control (channel \#1) \[param1=Volume\]

</li>

<li>

**A1** Volume control (channel \#2) \[param1=Volume\]

</li>

<li>

**A2** Volume control (channel \#3) \[param1=Volume\]

</li>

<li>

**A3** Volume control (channel \#4) \[param1=Volume\]

</li>

<li>

**A4** Volume transition (channel \#1) \[param1=Transition time, param2=Target volume\]

</li>

<li>

**A5** Volume transition (channel \#2) \[param1=Transition time, param2=Target volume\]

</li>

<li>

**A6** Volume transition (channel \#3) \[param1=Transition time, param2=Target volume\]

</li>

<li>

**A7** Volume transition (channel \#4) \[param1=Transition time, param2=Target volume\]

</li>

<li>

**A8** Pan control (channel \#1) \[param1=Panning\]

</li>

<li>

**A9** Pan control (channel \#2) \[param1=Panning\]

</li>

<li>

**AA** Pan control (channel \#3) \[param1=Panning\]

</li>

<li>

**AB** Pan control (channel \#4) \[param1=Panning\]

</li>

<li>

**AC** Pan transition (channel \#1) \[param1=Transition time, param2=Target panning\]

</li>

<li>

**AD** Pan transition (channel \#2) \[param1=Transition time, param2=Target panning\]

</li>

<li>

**AE** Pan transition (channel \#3) \[param1=Transition time, param2=Target panning\]

</li>

<li>

**AF** Pan transition (channel \#4) \[param1=Transition time, param2=Target panning\]

</li>

------------------------------------------------------------------------

<li>

**B0** Tempo control (channel \#1) \[param1=Tempo\]

</li>

<li>

**B1** Tempo control (channel \#2) \[param1=Tempo\]

</li>

<li>

**B2** Tempo control (channel \#3) \[param1=Tempo\]

</li>

<li>

**B3** Tempo control (channel \#4) \[param1=Tempo\]

</li>

<li>

**B4** Tempo transition (channel \#1) \[param1=Transition time, param2=Target tempo\]

</li>

<li>

**B5** Tempo transition (channel \#2) \[param1=Transition time, param2=Target tempo\]

</li>

<li>

**B6** Tempo transition (channel \#3) \[param1=Transition time, param2=Target tempo\]

</li>

<li>

**B7** Tempo transition (channel \#4) \[param1=Transition time, param2=Target tempo\]

</li>

<li>

**B8** Volume control for channel \#1 to \#4 \[param1=Volume\]

</li>

<li>

**B9** Volume transition for channel \#1 to \#4 \[param1=Transition time, param2=Target volume\]

</li>

<li>

**BA** Pan control for channel \#1 to \#4 \[param1=Panning\]

</li>

<li>

**BB** Pan transition for channel \#1 to \#4 \[param1=Transition time, param2=Target panning\]

</li>

<li>

**BC** Tempo control for channel \#1 to \#4 \[param1=Tempo\]

</li>

<li>

**BD** Tempo transition for channel \#1 to \#4 \[param1=Transition time, param2=Target tempo\]

</li>

------------------------------------------------------------------------

<li>

**C0** Music volume \[param1=Volume\]

</li>

<li>

**C1** Music volume transition \[param1=Transition time, param2=Target volume\]

</li>

<li>

**C2** Music From-To volume transition \[param1=Transition time, param2=Starting volume, param3=Ending volume\]

</li>

------------------------------------------------------------------------

<li>

**C8** Music balance \[param1=balance\]

</li>

<li>

**C9** Music balance transition \[param1=Transition time, param2=Target balance\]

</li>

<li>

**CA** Music From-To balance transition \[param1=Transition time, param2=Starting balance, param3=Ending balance\]

</li>

------------------------------------------------------------------------

<li>

**D0** Music tempo \[param1=Tempo\]

</li>

<li>

**D1** Music tempo transition \[param1=Transition time, param2=Target tempo\]

</li>

<li>

**D2** Music From-To tempo transition \[param1=Transition time, param2=Starting tempo, param3=Ending tempo\]

</li>

------------------------------------------------------------------------

<li>

**F0** Stop music

</li>

<li>

**F1** Stop sound effects (channel \#1 to \#4)

</li>

</ul>

#### Please Note

Channel \#5 (used from operation 0x30) is dedicated to the menu and should not be used for anything else.  
All transitions use the formula Transition_time (in seconds) = param1 / 60.  
The pan (audio L/R balance) value range is 0 to 127, where 0 is fully left, 64 is centre, and 127 is fully right.  
The maximum volume is 127.  
The tempo value range is 0 to 127. The normal tempo is 0.  
Operations 0x10/14/18/19 do not work on the PSX game from field script \[CURRENTLY CHECKING THIS\].  
Operations 0xC8/C9/CA are not implemented in the PSX version or PC version despite the field script calling them.  
