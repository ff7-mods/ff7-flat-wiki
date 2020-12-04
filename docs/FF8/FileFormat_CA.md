---
title: FileFormat_CA
---

By myst6re.

## Camera

The format is almost the same as [Final Fantasy VII](../FF7/Field/Camera_Matrix.md). Differences:

-   The zoom can be present twice
-   There may be several cameras, in this case the camera structure is repeated several times, and sizeof(each struct) = 0x28 (with zoom twice for each)
