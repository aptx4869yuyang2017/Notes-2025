---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[优化DAX-CH16 理解权限优化]]"
created: 2025-02-06
tags:
---

![image.png](https://s1.vika.cn/space/2025/02/06/5d6d3878eede4c198f4444660d2f4510)
![image.png](https://s1.vika.cn/space/2025/02/06/be30d2a4514c475db4bdc6e5f07899f6)


```S03.M07.L03.D03
DEFINE
    MEASURE Sales[# Products] =
        DISTINCTCOUNT ( Sales[ProductKey] )

EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Brand],
    "Sales Amount", [Sales Amount],
    "# Products", [# Products]
)

```

![image.png](https://s1.vika.cn/space/2025/02/06/700774196e4a45b9ac18595cae1da692)
![image.png|469](https://s1.vika.cn/space/2025/02/06/9c6eae3a21074f3fb426a25040f234f8)

**与 Customer 的 JOIN 和过滤 Customer[Continent] 的条件都会添加到每个 xmSQL 查询中**


极端情况下，甚至会使用 Callback 调用 FE

`FIND ( "Europe", Customer[Continent], 1, - 1 ) <> -1`  *S03.M07.L03.D04*
