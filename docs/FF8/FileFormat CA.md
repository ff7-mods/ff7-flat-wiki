---
title: FileFormat CA
permalink: FileFormat CA.html
---

[Home](../Main%20Page.md) > [FF8](../FF8.md) > FileFormat CA

By myst6re.

## Camera

The format is almost the same as [Final Fantasy VII][]. Differences:

-   The zoom can be present twice
-   There may be several cameras, in this case the camera structure is
    repeated several times, and sizeof(each struct) = 0x28 (with zoom
    twice for each)

  [Final Fantasy VII]: ../FF7/Field/Camera%20Matrix.md "wikilink"
