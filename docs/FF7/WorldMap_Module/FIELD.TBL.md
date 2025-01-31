---
title: FIELD.TBL
---

## General

This file contains the definition of what field map should be loaded and also the coordinates to which the character should begin at when the () opcode is executed during world scripting.

## Contents

This file contains 64 records of 24 bytes each, they correspond to the 64 WM\* fields, but they work in the opposite direction. Each 24 byte record contains 2 scenarios, which are 12 bytes a piece, and indicated by the second parameter. Each scenario contains the Field Id for the field that it should jump to, this is at offset 0x6. For instance, when walking into North Corel, there are two possible fields that it can jump to; if you fail the Corel Train mission, it will jump to ncorel2 map instead of ncorel. The other data in this record is coordinates within the field to which your character will be initiated and also the starting direction your character is facing. For instance, the Chocobo Farm can be entered from the bottom or from the side, depending on certain flags set within your file game save.

## Structure

- **Short** *X*: X-coordinate of the player on the next field.
- **Short** *Y*: Y-coordinate of the player on the next field.
- **Short** *T*: Triangle ID of the player on the next field.
- **UShort** *F*: Field ID of the field to jump to.
- **UByte** *D*: Direction the character will be facing on the next field, in the standard game format.
- **3xUByte** *?*: All 3 bytes exactly match the previous byte

Offset to scenario record = ((Field Table Id - 1) \* 24) + (Scenario \* 12) Length = ALWAYS 12 bytes

## Additional Info

Another note of interest: As mentioned, there are 64 entries in FIELD.TBL, which correspond with the 64 WM fields. As known, when transitioning from field maps to the world map, the game uses 64 dummy-type fields to indicate 64 different points of entry (per coordinates) to the world map (some of which are relative coordinates to where you last were on the world map). These are NOT stored in FIELD.TBL. Instead they are stored in the System function ID 0 in the [worldmap scripts](Script#Functions). It is also important to note that all entry points map exactly to the exit points; that is, when you are leaving Midgar, you are in map mds5_5 and it MAPJUMPs to wm0, which puts you on the south side of Midgar, but when you walk into Midgar from the world map, it'll be record 0 in FIELD.TBL, which directs the game to jump to mds5_5.
