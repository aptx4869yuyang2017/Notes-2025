---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-All & AllExcept]]"
created: 2025-01-28
tags:
  - domain/powerbi
---

> [!important]  Top 类别子类别
> EN-P66/CH-P62
> 
> the category and subcategory of products that sold more than twice the average sales amount
> 销售额超过平均销售额两倍的产品类别和子类别
> 
> 怎么用 Calculate 写更更短/更高效的版本呢？


^f02df8



显示销售额超过平均值两倍的类别和子类别， 存到一个表中

- 使用 All 列出所有 类别-自类别组合
- 计算 类别-子类别组合 销售额 的平均值
- 筛选出 符合条件 的类别-子类别组合
	- 这里 创建变量的方式很有意思，要理解 **变量计算使用的是创建时候的计值上下文**

#### 方案一 - CH03版本

- 这里只是作为一个 说明 All 函数功能的案例
- 注意这里甚至没有用到上下文转换，是使用 不复用度量值 + RelatedTable 的方式利用 [[DAX-迭代函数]] AverageX

```
BestCategories =
VAR Subcategories =
    ALL ( 'Product'[Category], 'Product'[Subcategory] )
VAR AverageSales =
    AVERAGEX (
        Subcategories,
        SUMX ( RELATEDTABLE ( Sales ), Sales[Quantity] * Sales[Net Price] )
    )
VAR TopCategories =
    FILTER (
        Subcategories,
        VAR SalesOfCategory =
            SUMX ( RELATEDTABLE ( Sales ), Sales[Quantity] * Sales[Net Price] )
        RETURN
            SalesOfCategory >= AverageSales * 2
    )
RETURN
    TopCategories
```


#### 方案二 - 预计算版本

```
VAR Subcategories =
    ALL('Product'[Category], 'Product'[Subcategory])
VAR SalesPerSubcategory =
    ADDCOLUMNS(
        Subcategories,
        "@TotalSales", SUMX(RELATEDTABLE(Sales), Sales[Quantity] * Sales[Net Price])
    )
VAR AverageSales =
    AVERAGEX(SalesPerSubcategory, [@TotalSales])
VAR TopCategories =
    FILTER(
        SalesPerSubcategory,
        [@TotalSales] >= AverageSales * 2
    )
RETURN
    TopCategories

```


#### 方案三 -  使用 Calculate 预计算 (上下文转换)

```
VAR Subcategories =
    ALL('Product'[Category], 'Product'[Subcategory])

VAR AverageSales =
    AVERAGEX(
        Subcategories,
        CALCULATE(
            SUMX(Sales, Sales[Quantity] * Sales[Net Price])
        )
    )

VAR TopCategories =
    FILTER(
        Subcategories,
        CALCULATE(
            SUMX(Sales, Sales[Quantity] * Sales[Net Price])
        ) >= AverageSales * 2
    )

RETURN
    TopCategories

```

这个方案还是算了两遍 不是最优的