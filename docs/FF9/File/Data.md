---
title: Data
---

[Home](../../Main_Page.md) > [FF9](../../FF9.md) > [File](../File.md) > Data

Almost all files in FF9 has structure, which starts from 2 bytes DB (hex numbers). This record points, that after we'll have pointer list, which points to different data sections in the file (data can be sounds, TIMs, models, etc).

**DB Structure:**

|          Data          |           Size            |
|:----------------------:|:-------------------------:|
|          "DB"          |          1 byte           |
|     Pointers count     |          1 byte           |
|         00 00          |          2 bytes          |
| Pointer1, Pointer2,... | 4 bytes \* Pointers count |

Pointer is a number, which represent how many bytes from current position there is target data. Current position in this case is first byte of this pointer.

**Pointer structure:**

|   Data    |  Size   |
|:---------:|:-------:|
|  Pointer  | 3 bytes |
| Data Type | 1 byte  |

Data, where points this pointer begins with 2 bytes, first byte indicates, what data type we have, and second is count of objects of selected type.

**Data** **Data structure:**

|         |                                   |
|---------|-----------------------------------|
| 1 byte  | Data type                         |
| 1 byte  | Number of object\`s in this scope |
| 2 bytes | 00 00 (for 4 bytes align)         |

***Objects identifiers***

After this goes object identifiers for selecting in scripts.

One identifier are **2 bytes**, and size of all identifiers must be **aligned to 4 bytes** (by add 0000 identifier).

Identifiers count = Number of object\`s in Data Structure.

***Pointers to objects***

Count of pointers = Number of object\`s in Data Structure.

Size of all pointers are **4 bytes**.

Pointers are from current position (offset of current pointer + pointer value)

***End\`s pointer for objects***

After Pointers to objects goes **4 bytes**.

It\`s pointer from first pointer offset to end of last object (offset of first pointer + end\`s pointer)
