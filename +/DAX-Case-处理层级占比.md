---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH11 处理层级]]"
created: 2025-02-07
tags:
  - domain/powerbi
---

# 传统写法

[[DAX-IsInScope]]

```
PercOnParent = 
VAR CurrentSales = [Sales Amount]
VAR SubcategorySales = 
    CALCULATE (
        [Sales Amount],
        ALLSELECTED ( Product[Product Name] )
    )
VAR CategorySales = 
    CALCULATE (
        [Sales Amount],
        ALLSELECTED ( Product[Subcategory] )
    )
VAR TotalSales = 
    CALCULATE (
        [Sales Amount],
        ALLSELECTED ( Product[Category] )
    )
VAR RatioToParent =
IF (
    ISINSCOPE ( Product[Product Name] ),
    DIVIDE ( CurrentSales, SubcategorySales ),
    IF ( 
        ISINSCOPE ( Product[Subcategory] ),
        DIVIDE ( CurrentSales, CategorySales ),
        IF (
            ISINSCOPE ( Product[Category] ),
            DIVIDE ( CurrentSales, TotalSales )
        )
    )
)
RETURN RatioToParent
```


# 视觉计算


```
PercOnParent v2 = format(DIVIDE([Sales Amount], COLLAPSE([Sales Amount], ROWS)), "0 %")
```



