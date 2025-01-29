---
up:
  - "[[DAX-Calculate]]"
related: 
created: 2025-01-28
tags:
---

**21-03 引入了同表多条件筛选**
[Specifying multiple filter conditions in CALCULATE - SQLBI](https://www.sqlbi.com/articles/specifying-multiple-filter-conditions-in-calculate/)

# 简介

- 单表单列  `Sales[Net Price] >= 10 && Sales[Net Price] <= 100)`
- 单表多列 `Sales[Quantity] ** Sales[Net Price] >= 1000)` **版本更新后支持，有两种写法**
- 多表多列 只能使用 CrossJoin

```
Red or Contoso Sales :=
CALCULATE (
    [Sales Amount],
    'Product'[Color] = "Red" || 'Product'[Brand] = "Contoso"
)
 
Big Sales Amount :=
CALCULATE (
    [Sales Amount],
    KEEPFILTERS ( Sales[Quantity] * Sales[Net Price] > 1000 )
)
```

- 注意新增加的效果，也只是支持**同一张表上的多条件**


# 筛选上下文覆盖情况


```
DEFINE
    MEASURE Sales[Big Sales Amount] =
        CALCULATE (
            [Sales Amount],
            KEEPFILTERS ( Sales[Quantity] * Sales[Net Price] > 1000 )
        )
    MEASURE Sales[Big Sales Amount Overrides Filter] =
        CALCULATE (
            [Sales Amount],
            Sales[Quantity] * Sales[Net Price] > 1000
        )
EVALUATE
SUMMARIZECOLUMNS (
    Sales[Quantity],
    "Sales Amount", [Sales Amount],
    "Big Sales Amount", [Big Sales Amount],
    "Big Sales Amount Overrides Filter", [Big Sales Amount Overrides Filter]
)
```

![image.png](https://s1.vika.cn/space/2025/01/28/24bf51c88f1b493f91bf1259dd8c414a)

还是需要注意筛选覆盖的效果，所以一般还是要使用 [[DAX-KeepFilters]]


# 非同表的条件怎么办

使用 [[DAX-CrossJoin]] 

```
DEFINE
    MEASURE Sales[Sales Multiple or Red] =
        CALCULATE (
            [Sales Amount],
            FILTER (
                CROSSJOIN ( ALL ( Sales[Quantity] ), ALL ( 'Product'[Color] ) ),
                Sales[Quantity] > 1 || 'Product'[Color] = "Red"
            )
        )
EVALUATE
SUMMARIZECOLUMNS (
    'Product'[Brand],
    "Sales Amount", [Sales Amount],
    "Sales Multiple or Red", [Sales Multiple or Red]
)
```

![image.png](https://s1.vika.cn/space/2025/01/28/4e0e31ea821d45d28e249e4ad8851e7e)



# 最佳实践有变化么？



> [!important] 最佳实践
> **filter columns, don’t filter tables**
> 筛选列，不要筛选表


*更差*
```
Red Contoso Sales Bad Practice :=
CALCULATE (
    [Sales Amount],
    'Product'[Color] = "Red" && 'Product'[Brand] = "Contoso"
)
```

**更好**
```
Red Contoso Sales :=
CALCULATE (
    [Sales Amount],
    'Product'[Color] = "Red",
    'Product'[Brand] = "Contoso"
)
```