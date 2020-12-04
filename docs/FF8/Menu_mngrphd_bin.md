---
title: Menu_mngrphd_bin
---

This is the map for [mngrp.bin](Menu_mngrp_bin.md). Locations to data and the size of the section.

## Entry

| Type   | Size | Value | Description                                                                                                                                                                    |
|--------|------|-------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UInt32 | 4    | Seek  | Location of data. This value is **1 more** than the actual location. So may want to **subtract 1** from these values when reading file. (**{0xFFFFFFFF}** values are invalid.) |
| UInt32 | 4    | Size  | Total Size of all data at this location. (**{0x00000000}** values are invalid.)                                                                                                |
