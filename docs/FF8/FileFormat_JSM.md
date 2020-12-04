---
title: FileFormat_JSM
---

By myst6re.

## Fields Scripts

| Offset           | Size                               | Data                                                                 |
|------------------|------------------------------------|----------------------------------------------------------------------|
| 0                | 1 byte                             | Count of door entity                                                 |
| 1                | 1 byte                             | Count of walkmesh line entity                                        |
| 2                | 1 byte                             | Count of background entity                                           |
| 3                | 1 byte                             | Count of other entity                                                |
| 4                | 2 bytes                            | Offset section 1                                                     |
| 6                | 2 bytes                            | Offset script data                                                   |
| 8                | offsetSection1 - 8 = nbEntity \* 2 | [Entry point of each entity](#entry-point-of-each-entity) |
| offsetSection1   | offsetScriptData - offsetSection1  | [Entry point of each script](#entry-point-of-each-script) |
| offsetScriptData | varies                             | [Script Data](#script-data)                               |

### Entry point of each entity

Each entry is 2 bytes with:

      scriptCount = entryPointEntity & 0x7F;
      label = entryPointEntity >> 7;

The entry points are sorted in order of execution (I guess), not in the order in which entities appear in the file.

When sorting entities, it will be always in that order:

1.  Lines
2.  Doors
3.  Backgrounds
4.  Other

To know what type of an entity, so we were just use their count.

### Entry point of each script

Each entry is 2 bytes with:

      position = (entryPointScript & 0x7FFF)*4;
      flag = entryPointScript >> 15;

The position is relative to *offsetScriptData*. The meaning of the flag is unknown, it appear always and only with door, location and background entities. Last entry point is relative EOF

### Script Data

Each opcode is 4 bytes.

[Opcode List](Field/Script/Opcodes.md)
