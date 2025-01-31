---
title: 38_STTIM
---

- Opcode: **0x38**
- Short name: **STTIM**
- Long name: Set Timer

#### Memory layout

| 0x38 | *B1 / B2* | *0 / B3* | *H* | *M* | *S* |
|------|-----------|----------|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to find hours value, or zero if hours (*B1*) is passed as a value.
- **const Bit\[4\]** *B2*: Bank to find minutes value, or zero if minutes (*B2*) is passed as a value.
- **const Bit\[4\]** *0*: Zero.
- **const Bit\[4\]** *B3*: Bank to find seconds value, or zero if seconds (*B3*) is passed as a value.
- **const UByte** *H*: Hours, or address to find hours value, if *B1* is non-zero.
- **const UByte** *M*: Minutes, or address to find minutes value, if *B2* is non-zero.
- **const UByte** *S*: Seconds, or address to find seconds value, if *B3* is non-zero.

#### Description

Sets the clock, as found in the [WSPCL](36_WSPCL) opcode.

If the hours, minutes or seconds are specified in the argument, the corresponding *B* nybble is zero. Otherwise, the value for the time component is retrieved from the bank and address specified. The seperate time components can be retrieved from memory or specified as a value, in the same argument list, as demonstrated below.

Hours are not directly visible on the clock, as it only displays minutes and seconds. Hours are translated into minutes, so if you specify one hour, the clock displays 60 minutes, and so on.

#### Example

The following example sets the clock to 67:34 using literal values for hours, and retrieved values for minutes and seconds.

`SETBYTE(50,12,7)             // Bank 5, Address 0x12: 7 minutes`  
`SETBYTE(50,14,22)            // Bank 5, Address 0x14: 34 seconds`  
`STTIM(5,5,1,12,14)           // One hour, retrieved vals for minutes/seconds`  
`WINDOW(0,20,20,75,75)        // Set up a window`  
`WSPCL(0,1,5,5)               // Set the window to a timer type`  
`WMODE(0,2,1)                 // Transparent, non-closable window`  
`MESSAGE(0,1)                 // Display the window & timer`
