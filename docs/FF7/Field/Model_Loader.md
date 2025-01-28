---
title: Model_Loader
---

## Model loader (FF7 PC)

| Offset | Size                   | Data                 |
|--------|------------------------|----------------------|
| 0      | 2                      | *Always 0*           |
| 2      | 2                      | Model count          |
| 4      | 2                      | Model scale (unused) |
| 6      | *varies* \* modelCount | Model Loader data    |

## Model loader data

For each model:

| Offset | Size | Data |
|----|----|----|
| 0 | 2 | Size of model name string |
| 2 | SizeModelName | Model name (*fieldNameModel_name.char*, unused) |
| 2 + SizeModelName | 2 | Unknown (sometimes 0 if the model is playable, 1 otherwise) |
| 4 + SizeModelName | 8 | HRC name (AAAA.HRC for example) |
| 12 + SizeModelName | 4 | Model scale string |
| 16 + SizeModelName | 2 | Number of animations |
| 18 + SizeModelName | 3 | Light color 1 (RGB format) |
| 21 + SizeModelName | 2 \* 3 | Light coordinates? 1 (signed short) |
| 27 + SizeModelName | 3 | Light color 2 (RGB format) |
| 30 + SizeModelName | 2 \* 3 | Light coordinates? 2 (signed short) |
| 36 + SizeModelName | 3 | Light color 3 (RGB format) |
| 39 + SizeModelName | 2 \* 3 | Light coordinates? 3 (signed short) |
| 45 + SizeModelName | 3 | Global light color (RGB format) |
| 48 + SizeModelName | *varies* \* animationCount | Loaded Animations |

### Loaded animations

| Offset | Size | Data |
|----|----|----|
| 0 | 2 | Size of animation name string |
| 2 | SizeAnimName | Animation name (file name extension can be removed) |
| 2 + SizeAnimName | 2 | Unknown |
