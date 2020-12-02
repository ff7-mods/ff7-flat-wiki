---
title: sector
---

[Home](/Main%20Page.md) > [FF9](/FF9.md) > [glossary](/FF9/glossary.md) > sector

A sector refers to a ISO9660 Data Block size. This varies between modes
and forms within the ISO format. However Playstation disk were recorded
specifically in Mode 2 format. So a Sector would be Mode 2 form 1 or 2
data blocks, which are 2048 (2K) or 2324 bytes in size respectively. In
general data is 2K in size only data that needs to be dma'd through the
PS1's audio decoding hardware needs to use the 2324byte sector size.
