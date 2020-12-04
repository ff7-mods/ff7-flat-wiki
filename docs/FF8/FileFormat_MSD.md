---
title: FileFormat_MSD
---

By myst6re.

## Field texts

This file contains just a list of positions for each text, and text data. If you want to calculate the number of texts, you can do this:

    nbText = firstTextPos / 4

| Offset   | Size   | Data               |
|----------|--------|--------------------|
| 0        | 4      | Position of text 1 |
| ...      | ...    | ...                |
| varies   | 4      | Position of text N |
| textPos1 | varies | Text data 1        |
| ...      | ...    | ...                |
| textPosN | varies | Text data N        |
