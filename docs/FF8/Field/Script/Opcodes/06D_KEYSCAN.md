---
title: 06D_KEYSCAN
---

-   Opcode: **0x06D**
-   Short name: **KEYSCAN**
-   Long name: Scan for pressed key

#### Argument

none

#### Stack

  
*Key flags*

**KEYSCAN**

#### Key Flags

  
16: Cancel

32: Menu

64: OK/Accept

128: Card game button (I think it's called "switch")

#### Description

Writes 1 to temporary variable 0 (access with PSHI\_L 0) if the user is pressing any of the indicated keys. 0 otherwise. The script does not pause while doing this, so you have to run it in a touch or push script, or inside a looping subroutine.
