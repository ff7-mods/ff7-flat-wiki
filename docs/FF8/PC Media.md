---
title: PC Media
permalink: PC Media.html
---

[Home](../Main%20Page.md) > [FF8](../FF8.md) > PC Media

# Data File Format

Located in the <installation folder>\\Data\\ folder, there are five (or
six for the maximum installation) sets of three files.

### .fs (File Source)

This is the main data source for all the files in a given category. The
files are either [LZSed][] or left raw (See notes on .fi files) and all
concatenated together.

### .fl (File List)

This is a simple flatfile using a DOS-style text encoding (uses both
Carriage\_Return and Line\_Feed to indicate a new line) containing a
sequential list of absolute paths and file names of the files stored in
the .fs file.

### .fi (File Index)

For each file in the .fs archive, there are 3 Long Words (12 bytes) of
data in this file.

| Data                                     | Offset |
|------------------------------------------|--------|
| Length of unpacked file                  | 0x00   |
| Location of packed file with .fs archive | 0x04   |
| Compression used (1 = LZS; 0 = None)     | 0x08   |

  [LZSed]: ../FF7/Kernel/Low%20level%20libraries.md#LZS%20Archives "wikilink"
