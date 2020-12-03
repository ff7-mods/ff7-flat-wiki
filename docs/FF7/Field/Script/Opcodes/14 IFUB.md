---
title: 14 IFUB
---

[Home](../../../../Main%20Page.md.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 14 IFUB

-   Opcode: **0x14**
-   Short name: **IFUB**
-   Long name: If (Unsigned Byte)

#### Memory layout

| 0x14 | *B1 / B2* | *A* | *V* | *C* | *E* |
|------|-----------|-----|-----|-----|-----|

#### Arguments

-   **const Bit\[4\]** *B1*: First memory bank to access.
-   **const Bit\[4\]** *B2*: Second memory bank to access.
-   **const UByte** *A*: Address, from the first bank, of the value to
    retrieve.
-   **const UByte** *V*: Unsigned value to compare the retrieved value
    to, or address from the second bank of the value to retrieve.
-   **const UByte** *C*: Type of comparison to perform.
-   **const UByte** *E*: Amount to jump if the comparison does not hold.

#### Description

Performs a comparison between a retrieved values from memory at specific
banks and addresses. If **B2** is zero, then the value retrieved from
bank **B1**, address **A** is compared with the value specified by
**V**. If **B2** is not zero, then the value retrieved from bank **B1**,
address **A** is compared with the value retrieved from bank **B2**,
address **V**.

The type of comparison used is shown in the table below. If the
comparison fails, the script pointer jumps forward by the amount
specified in the final argument; the starting offset for this jump is
just before the jump value argument itself. This, combined with an
appropriate [jump forward][], is used to implement if/else functionality
in scripts, as demonstrated below.

If the content of the 'if' block following the IFUB line is longer than
0xFF, the jump argument will also need to be longer than 0xFF, and hence
the [IFUBL][] variant is used instead. If the value to compare is larger
than 0xFF, the [IFUW][]/[IFUWL][] variants are used. If the value being
compared is negative, the [IFSW][]/[IFSWL][] variants are used.

#### Comparison Types

| ID  | Comparison Performed  |
|-----|-----------------------|
| 0   | A == B                |
| 1   | A != B                |
| 2   | A &gt; B              |
| 3   | A &lt; B              |
| 4   | A &gt;= B             |
| 5   | A &lt;= B             |
| 6   | A & B                 |
| 7   | A ^ B                 |
| 8   | A \| B                |
| 9   | A & (1&lt;&lt;B)      |
| A   | !((A & (1&lt;&lt;B))) |
|     |                       |

#### If/Else Example

In this example, if the value found is greater than 0x30, the script
halts for a shorter period of time; otherwise, the script halts for a
long period of time. Note how the jump forward placed before the longer
WAIT (start of the required 'else' block) ensures that on completion of
the 'if' block, execution of the 'else' block is avoided. It jumps
forward to just before the 0x200 WAIT, which it then executes, and
returns.

The 'else' block only executes if it is jumped into by the final
argument of the IFUB argument list (thus avoiding the execution of the
'if' block). Once the 'else' block is executed, script execution just
continues and the 0x200 WAIT and RET is executed. Since this is also
executed by the 'if' block having jumped forward to skip the else block,
this demonstrates that the two code paths converge. In C++ (below) this
is the equivalent of the if/else block being completed.

    IFUB (10,20,30,02,06)
    WAIT (00,01)
    JMPF (04)
    WAIT (00,04)
    WAIT (00,02)
    RET ()

<cpp>

`if(<10>[20] > 30)`  
`{`  
` WAIT(100);`  
`}`  
`else`  
`{`  
` WAIT(400);`  
`}`

`WAIT(200);`  
`return;`

</cpp>

  [jump forward]: 10%20JMPF.md "wikilink"
  [IFUBL]: 15%20IFUBL.md "wikilink"
  [IFUW]: 18%20IFUW.md "wikilink"
  [IFUWL]: 19%20IFUWL.md "wikilink"
  [IFSW]: 16%20IFSW.md "wikilink"
  [IFSWL]: 17%20IFSWL.md "wikilink"
