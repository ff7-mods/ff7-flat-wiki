---
title: FIELD.TBL
---

## General

This file contains 64 records of 24 bytes each, they correspond to the 64 WM\* fields, but they work in the opposite direction. Each 24 byte record contains 2 scenarios, which are 12 bytes a piece, and indicated by the second parameter. Each scenario contains the Field Id for the field that it should jump to, this is at offset 0x6. For instance, when walking into North Corel, there are two possible fields that it can jump to; if you fail the Corel Train mission, it will jump to ncorel2 map instead of ncorel. The other data in this record is unknown, but does contains coordinates within the field to which your character will be initiated. For instance, the Chocobo Farm can be entered from the bottom or from the side, depending on certain flags set within your file game save.

Offset to scenario record = (Field Table Id) \* 24 + (Scenario \* 12) Length = ALWAYS 12 bytes

Another note of interest: As mentioned, there are 64 entries in FIELD.TBL, which correspond with the 64 WM fields. As known, when transitioning from field maps to the world map, the game uses 64 dummy-type fields to indicate 64 different points of entry (per coordinates) to the world map (some of which are relative coordinates to where you last were on the world map). The coordinates that it transports to are currently unknown, but likely contained within FIELD.TBL. It is also important to note that all entry points map exactly to the exit points; that is, when you leave Midgar, you are in map mds5_5 and it MAPJUMPs to wm0, which puts you on the south side of Midgar, but when you walk into Midgar from the world map, it'll be record 0 in FIELD.TBL, which directs the game to jump to mds5_5.
