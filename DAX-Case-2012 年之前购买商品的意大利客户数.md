---
up:
  - "[[DAX-Calculate-筛选参数的执行顺序]]"
related:
  - "[[DAX-Calculate]]"
created: 2025-01-29
tags:
  - domain/powerbi
---
# 方案一 

- 计值目标：购买过商品的客户，使用 Filter + 上下文转换
- 意大利客户作为 Calculate 条件

```
CALCULATE (
    COUNTROWS (
        FILTER (
            Customer,
            CALCULATE (
                SUM ( Sales[Amount] ),
                YEAR ( Sales[Date] ) < 2012
            ) > 0
        )
    ),
    KEEPFILTERS ( Customer[Country] = "Italy" )
)
```

# 方案二

计值目标：`COUNTROWS ( Customer )`
Calculate 条件
 - 条件1:购买过商品的部分作为度量值
- 条件2:意大利客户作为 

```
CALCULATE (
    COUNTROWS ( Customer ),
    FILTER (
        Customer,
        CALCULATE (
            SUM ( Sales[Amount] ),
            YEAR ( Sales[Date] ) < 2012
        ) > 0
    ),
    KEEPFILTERS ( Customer[Country] = "Italy" )
)
```

# 方案三


- Calculate 外层：意大利客户
- Calculate 内层
	- 计值 `COUNTROWS ( Customer )`
	- 条件：购买过商品 （也受到 外层 Calcualte 影响）

```
CALCULATE (
    CALCULATE (
        COUNTROWS ( Customer ),
        FILTER (
            Customer,
            CALCULATE (
                SUM ( Sales[Amount] ),
                YEAR ( Sales[Date] ) < 2012
            ) > 0
        )
    ),
    KEEPFILTERS ( Customer[Country] = "Italy" )
)
```