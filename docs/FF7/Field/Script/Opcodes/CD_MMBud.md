---
title: CD_MMBud
---

- Opcode: **0xCD**
- Short name: **MMBud**
- Long name: Member Block +/- (Party Select: Character Switch)

#### Memory layout

| 0xCD | *S* | *C* |
|------|-----|-----|

#### Arguments

- **const UByte** *S*: Switches the character on/off (1/0, respectively).
- **const UByte** *C*: Character ID whose status will change.

#### Description

Enables or disables the availability of this character in the game, as well as in the right-hand selector pane in the party select menu. If the character is currently in the party, this will have no effect as the character is already displayed in the current party list (left pane).

This turns the character on or off globally. That is, if you turn off the character and then query whether the character is available with [IFMEMBQ](CC_IFMEMBQ), the comparison will not hold, and the script will jump to the second argument of IFMEMBQ.

#### Character IDs

| ID  | Character |
|-----|-----------|
| 0   | Cloud     |
| 1   | Barret    |
| 2   | Tifa      |
| 3   | Aeris     |
| 4   | Red XIII  |
| 5   | Yuffie    |
| 6   | Cait Sith |
| 7   | Vincent   |
| 8   | Cid       |
|     |           |
