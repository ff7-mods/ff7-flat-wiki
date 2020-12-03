---
title: Menu areames dc1
---

[Home](../Main%20Page.md.md) > [FF8](../FF8.md) > Menu areames dc1

## Format

Same format as: **[Menu\_mngrp\_strings\_locations][]**

## Contents

Contains area strings. **Offsets\[Location number from save\]** gets the
string that shows on the menu/load/save screens. The special character
**0xE\#\#** is 2 bytes. Subtract **0xE20** and you get the desired in
**[namedec.bin][]**.

### Example

**0xE22- Alcauld Plains**, **0xE22** becomes **Balamb**, so final string
is **Balamb- Alcauld Plains**

  [Menu\_mngrp\_strings\_locations]: http://wiki.ffrtt.ru/index.php/FF8/Menu_mngrp_strings_locations
  [namedec.bin]: Main%20namedic.md "wikilink"
