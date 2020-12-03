---
title: FileFormat MSK
---

[Home](Main%20Page.md) > [FF8](FF8.md) > FileFormat MSK

By myst6re.

## Movie Cam?

| Offset | Size              | Data           |
|--------|-------------------|----------------|
| 0      | 4 bytes           | Count          |
| 4      | 24 \* Count bytes | Cam Positions? |

I think for "Count" frame, there are four points (4 \* 6 bytes = 4 \*
(x,y,z)) in space.
