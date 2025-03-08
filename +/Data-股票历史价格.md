---
up: 
related: 
created: 2025-02-24
tags:
---

# A 股

[AKShare 文档](https://fuakshare.akfamily.xyz/data/stock/stock.html#id21)

```
import akshare as ak

stock_zh_a_hist_df = ak.stock_zh_a_hist(
    symbol="000001", period="daily", start_date="20250201", end_date='20250223', adjust="hfq")
print(stock_zh_a_hist_df)
```

