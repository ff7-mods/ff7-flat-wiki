---
title: Menu_price_bin
---

### price.bin

Shop prices - 4 bytes per [item](Item_Codes.md)

| Type   | Size | Value           |
|--------|------|-----------------|
| UInt16 | 2    | Base Price      |
| UInt16 | 2    | Sell Multiplier |

Buy Price = Base Price \* 10

Sell Price = Base Price \* Sell Multiplier / 2
