---
title: 00_RET
---

- Opcode: **0x00**
- Short name: **RET**
- Long name: Return from request / Halt

#### Memory layout

| 0x00 |
|------|

#### Arguments

None.

#### Description

When an [entity](FF7/Field/Script/Entity "wikilink")'s script is being executed as part of a request (function call), the return opcode will cause current execution to halt and return to whatever the entity was previously executing (at some lower [priority](FF7/Field/Script/Priorities "wikilink")). If the execution was requested via a synchronous call ([REQEW](FF7/Field/Script/Opcodes/03_REQEW "wikilink") or [PRQEW](06_PRQEW), the completion of execution is also signalled to the calling entity which can resume execution.

If *return* is used when executing at base priority, execution will simply halt. This is what happens in the [entry scripts](../../Scripts/Entry_script).
