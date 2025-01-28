---
title: F5_ARROW
---

- Opcode: **0x0FF5**
- Short name: **SPECIAL: ARROW**
- Long name: Special: Arrow Switch

#### Memory layout

| 0x0F | 0xF5 | S   |
|------|------|-----|

#### Arguments

- **const UByte** *S*: Switch on/off (0/1, respectively).

#### Description

Turns on or off the *availability* of the hand pointer that hovers above the playable character's head; this does not do the same as pressing the Assist button, but rather toggles whether the hand will appear when the user has the hand and arrows set to display. Other indicators that are available, such as the red/green arrows that are turned on or off along with the hand pointer, are not affected by this sub-opcode.
