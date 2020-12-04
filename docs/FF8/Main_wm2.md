---
title: Main_wm2
---

By MaKiPL

  

## Info

**wm2field.tbl** is file that handles the world map to field warping.

## Structure

File is 1728 bytes. Where every entry is 24 bytes. Though 1728/24 = 72 entries

One entry:

| Offset | SizeOf       | Name     | Description     |
|--------|--------------|----------|-----------------|
| 0      | short        | FieldX   | Operates FieldX |
| 2      | short        | FieldY   | Operates FieldY |
| 4      | ushort (yes) | Field\_Z | Operates FieldZ |
| 6      | ushort       | FieldID  | ID of field     |
| 8      | 16 bytes     | UNKNOWN  | Unknown         |

  

## Field location

Old wiki page about wm2field stated, that X Y Z coordinates are based on 12 bits. No, they aren't, I made a mistake. They are normal WORDs with sign-extension for X and Y and Z is normal WORD copying and no cmp(0x7FFF), so it's unsigned. The axis are indeed X Y Z, not X-ZY as everywhere else in FF8. Byte after fieldID is some sort of pointer, currently unknown what is it purpouse.

## Useful notes

First entry is Balamb Garden

Second entry is Balamb City
