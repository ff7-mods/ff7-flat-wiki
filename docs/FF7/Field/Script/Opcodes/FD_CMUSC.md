---
title: FD_CMUSC
---

- Opcode: **0xFD**
- Short name: **CMUSC**
- Long name: Change Music

#### Memory layout

| 0xFD | *I* | *p1* | *p2* | *p3* | *p4* | *p5* | *p6* |
|------|-----|------|------|------|------|------|------|

#### Arguments

- **const UByte** *I*: Ref to music files for the field (field flevel-\>script-\>AKAO\[\]
- **const UByte** *p1*: Unknown, always 0 (PC)
- **const UByte** *p2*: Potentially fadeOut time from current music
- **const UByte** *p3*: Potentially fadeIn time and trigger from changed music
- **const UByte** *p4*: Unknown, always 0 (PC)
- **const UByte** *p5*: Unknown, always 0 (PC)
- **const UByte** *p6*: Unknown, always 0 (PC)

#### Description

Most commonly used for the sleeping at an inn. When p3 === 0 && p2 === 20, the current music stops immediately and the change music id plays at the channel volume immediately. When p3 \> 0 && p2 \> 20, the current music fades out (potentially at 20 frames - p2), after the fade has ended, the change music is faded in (potentially at 30 frames, p3)
