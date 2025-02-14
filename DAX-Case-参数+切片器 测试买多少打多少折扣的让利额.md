---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-设计模式(book)]]"
created: 2025-02-11
tags:
  - domain/powerbi
---

# 需求 1 

![image.png](https://s1.vika.cn/space/2025/02/11/e762295f50cb473aad5d994326d0452d)


# 构造表

```
Min Quantity = 
SELECTCOLUMNS (
    GENERATESERIES ( 1, 10, 1 ),
    "Min Quantity", [Value]
)
```

```
Discount = 
SELECTCOLUMNS (
    GENERATESERIES ( 0, 0.45, 0.05 ),
    "Discount", [Value]
)
```


# 度量值



```
Discounted Amount = 
VAR MinQty =
    SELECTEDVALUE ( 'Min Quantity'[Min Quantity], 1 )
VAR Disc =
    SELECTEDVALUE ( Discount[Discount], 0 )
VAR Orders =
    ADDCOLUMNS (
        SUMMARIZE ( Sales, Sales[Order Number] ),
        "@Qty", [# Quantity],
        "@Amt", [Sales Amount]
    )
VAR Result =
    SUMX (
        Orders,
        IF (
            [@Qty] >= MinQty,
            ( 1 - Disc ) * [@Amt],
            [@Amt]
        )
    )
RETURN
    Result
```


# 需求2 参数之间依赖

Discount 设计成可以被筛选的状态

![image.png](https://s1.vika.cn/space/2025/02/11/461d9121559b439ebead4950f6e3a7a6)


```
Discount = 
VAR Discounts =
    SELECTCOLUMNS ( GENERATESERIES ( 0, 19, 1 ), "Discount", [Value] / 20 )
VAR Quantities =
    SELECTCOLUMNS ( GENERATESERIES ( 1, 10, 1 ), "Min Quantity", [Value] )
RETURN
    GENERATE (
        Quantities,
        FILTER (
            Discounts,
            [Discount] <= [Min Quantity] / 10
        )
    )
```

![image.png|467](https://s1.vika.cn/space/2025/02/11/8f6e2436378a4031aba3c250b4cf80e7)
