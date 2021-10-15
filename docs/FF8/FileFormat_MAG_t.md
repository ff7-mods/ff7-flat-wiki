---
title: FileFormat_MAG_t
---

By MaKiPL

------------------------------------------------------------------------

This is just .TIM texture

Possible namings:

### Type A

XyN

X- Sequence number

y- Always t (Texture)

N- Index of texture in given sequence

Example:

1t2- Texture number two in sequence number one.

### Type A2

yNN

y- Always t (Texture)

NN- Index of texture overly

Example:

t02 - Texture number two in given file (no sequence naming)

### Type B (chaos like)

.NN

NN-index (digit)

Example:

.01

-   Note: yes, there's no texture sign in name

To know, how to find out if the given file is texture, please reffer to [MAGfiles\_Generic](FileFormat_magfiles.md)

### Type C (chaos like)

.N.dat

N-index (literal)

Example:

.a.dat

-   Note: yes, there's no texture sign in name

To know, how to find out if the given file is texture, please reffer to [MAGfiles\_Generic](FileFormat_magfiles.md)
