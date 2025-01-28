---
title: Models
---

## Structure

| Offset | Size            | Data              |
|--------|-----------------|-------------------|
| 0      | 2               | Size of section   |
| 2      | 2               | Model count       |
| 4      | 8 \* modelCount | Model Loader data |

## Model Loader data

| Offset | Size | Data |
|----|----|----|
| 0 | 1 | Face ID |
| 1 | 1 | Number of bones |
| 2 | 1 | Number of parts |
| 3 | 1 | Number of animations |
| 4 | 1 | Unknown |
| 5 | 1 | Non Playable Character? (sometimes 1, also present in the PC model loader) |
| 6 | 1 | Unknown |
| 7 | 1 | Global model ID (to find out which BCX to use) |
