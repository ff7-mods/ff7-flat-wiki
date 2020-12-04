---
title: Menu_areames_dc1
---

## Format

Same format as: **[Menu\_mngrp\_strings\_locations](http://wiki.ffrtt.ru/index.php/FF8/Menu_mngrp_strings_locations)**

## Contents

Contains area strings. **Offsets\[Location number from save\]** gets the string that shows on the menu/load/save screens. The special character **0xE\#\#** is 2 bytes. Subtract **0xE20** and you get the desired in **[namedec.bin](Main_namedic.md)**.

### Example

**0xE22- Alcauld Plains**, **0xE22** becomes **Balamb**, so final string is **Balamb- Alcauld Plains**
