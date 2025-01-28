---
title: 9C_2BYTE
---

- Opcode: **0x9C**
- Short name: **2BYTE**
- Long name: Two Byte Value

#### Memory layout

| 0x9C | *B1 / B2* | *B3* | *D* | *L* | *H* |
|------|-----------|------|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Destination bank.
- **const Bit\[4\]** *B2*: Bank to retrieve *L*, or zero if *L* is specified as a literal value.
- **const UByte** *B3*: Bank to retrieve *H*, or zero if *H* is specified as a literal value.
- **const UByte** *D*: Destination address.
- **const UByte** *L*: Low byte, or address to retrieve value if *B2* is non-zero.
- **const UByte** *H*: High byte, or address to retrieve value if *B3* is non-zero.

#### Description

Constructs and stores a two-byte value from two seperate one-byte values. The low and high bytes of the two-byte word may be taken from existing values from memory, or specified as a value (or both).
