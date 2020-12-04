---
title: FileFormat_r0win
---

By MaKiPL

------------------------------------------------------------------------

**R0win.dat** is loaded by the engine just after the battle ends with winning situation. This file is complete sequence and logic for battle winning scene.

Structure:

ENTRY

SECTION1

SECTION2 …

SECTION8

EOF

### ENTRY

<table><thead><tr class="header"><th><p><strong>Offset</strong></p></th><th><p><strong>Type</strong></p></th><th><p><strong>Name</strong></p></th></tr></thead><tbody><tr class="odd"><td><p>0</p></td><td><p>int</p></td><td><p>NumberOfSections</p></td></tr><tr class="even"><td><p>4</p></td><td><p>int</p></td><td><p>Section_1_pointer</p></td></tr><tr class="odd"><td><p>8</p></td><td><p>int</p></td><td><p>Section_2_pointer</p></td></tr><tr class="even"><td><p>12</p></td><td><p>int</p></td><td><p>Section_3_pointer</p></td></tr><tr class="odd"><td><p>16</p></td><td><p>int</p></td><td><p>Section_4_pointer</p></td></tr><tr class="even"><td><p>20</p></td><td><p>int</p></td><td><p>Section_5_pointer</p></td></tr><tr class="odd"><td><p>24</p></td><td><p>int</p></td><td><p>Section_6_pointer</p></td></tr><tr class="even"><td><p>28</p></td><td><p>int</p></td><td><p>Section_7_pointer</p></td></tr><tr class="odd"><td><p>32</p></td><td><p>int</p></td><td><p>Section_8_pointer</p></td></tr><tr class="even"><td><p>36</p></td><td><p>int</p></td><td><p>Section_to_EOF</p></td></tr></tbody></table>

### SECTION1 (sounds)

<table><thead><tr class="header"><th><p><strong>Offset</strong></p></th><th><p><strong>Type</strong></p></th><th><p><strong>Name</strong></p></th></tr></thead><tbody><tr class="odd"><td><p>0</p></td><td><p>int</p></td><td><p>NumberOfSounds</p></td></tr><tr class="even"><td><p>4</p></td><td><p>int</p></td><td><p>Pointer_to_AKAO1</p></td></tr><tr class="odd"><td><p>8</p></td><td><p>int</p></td><td><p>Pointer_to_AKAO2</p></td></tr><tr class="even"><td><p>16</p></td><td><p>AKAO</p></td><td><p>AKAO1 [Wind?] ??</p></td></tr><tr class="odd"><td><p>126160</p></td><td><p>AKAO</p></td><td><p>AKAO2 [Win]</p></td></tr></tbody></table>

### SECTION2 (camera animation)

For camera data structure please head over to [Battle stage model file](FileFormat_X.md)

### SECTION3 (UNKNOWN)

| Offset | Name               | Description                |
|--------|--------------------|----------------------------|
| 0      | Number of textures | Number of pointers in file |
| 4      | UNKNOWN            | Pointer to UNKNOWN data    |
| 8      | UNKNOWN            | Pointer to UNKNOWN data    |
| 12     | UNKNOWN            | Pointer to UNKNOWN data    |

### SECTION4,5,6,7,8 (UNKNOWN)

<table><thead><tr class="header"><th><p><strong>Offset</strong></p></th><th><p><strong>Type</strong></p></th><th><p><strong>Name</strong></p></th></tr></thead><tbody><tr class="odd"><td><p>0</p></td><td><p>int</p></td><td><p>NumberOfUNKNOWN</p></td></tr><tr class="even"><td><p>4</p></td><td><p>int</p></td><td><p>Pointer_to_UNK1</p></td></tr><tr class="odd"><td><p>8</p></td><td><p>int</p></td><td><p>Pointer_to_UNK2...</p></td></tr><tr class="even"><td><p>Varies from number of UNKNOWNs</p></td><td><p>int</p></td><td><p>EOF</p></td></tr></tbody></table>
