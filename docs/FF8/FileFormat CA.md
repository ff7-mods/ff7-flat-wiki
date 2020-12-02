---
title: FileFormat CA
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > FileFormat CA

By myst6re.

## Camera

The format is almost the same as [Final Fantasy VII][]. Differences:

-   The zoom can be present twice
-   There may be several cameras, in this case the camera structure is
    repeated several times, and sizeof(each struct) = 0x28 (with zoom
    twice for each)

  [Final Fantasy VII]: /ff7-flat-wiki/FF7/Field/Camera%20Matrix.md "wikilink"
