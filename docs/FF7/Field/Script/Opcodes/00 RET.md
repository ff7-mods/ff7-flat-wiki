---
title: 00 RET
---

[Home](../../../../Main%20Page.md.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 00 RET

-   Opcode: **0x00**
-   Short name: **RET**
-   Long name: Return from request / Halt

#### Memory layout

| 0x00 |
|------|

#### Arguments

None.

#### Description

When an [entity][]'s script is being executed as part of a request
(function call), the return opcode will cause current execution to halt
and return to whatever the entity was previously executing (at some
lower [priority][]). If the execution was requested via a synchronous
call ([REQEW][] or [PRQEW][]), the completion of execution is also
signalled to the calling entity which can resume execution.

If *return* is used when executing at base priority, execution will
simply halt. This is what happens in the [entry scripts][].

  [entity]: ../Entity.md "wikilink"
  [priority]: ../Priorities.md "wikilink"
  [REQEW]: 03%20REQEW.md "wikilink"
  [PRQEW]: 06%20PRQEW.md "wikilink"
  [entry scripts]: ../../Scripts/Entry%20script.md "wikilink"
