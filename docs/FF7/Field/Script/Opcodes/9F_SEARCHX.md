---
title: 9F_SEARCHX
---

- Opcode: **0x9F**
- Short name: **SEARCHX**
- Long name: Search into var map

#### Memory layout

| 0x9F | *B1 / B2* | *B3 / B4* | *0 / B6* | *Ofst* | *Start* | *End* | *V* | *R* |
|------|-----------|-----------|----------|--------|---------|-------|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank where to look.
- **const Bit\[4\]** *B2*: Bank to retrieve *Start*, or zero if *Start* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve *End*, or zero if *End* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank to retrieve *V*, or zero if *V* is specified as a literal value.
- **const Bit\[4\]** *0*: Zero.
- **const Bit\[4\]** *B6*: Bank to store Result.
- **const UByte** *Ofst*: Offset.
- **const UShort** *Start*: Start offset.
- **const UShort** *End*: End offset.
- **const UByte** *V*: Value to search.
- **const UByte** *R*: Result adress.

#### Description

Search the value *V* between *Ofst* + *Start* and *Ofst* + *End* in the bank *B1* and store the position in *R* if found, or -1 of not.
