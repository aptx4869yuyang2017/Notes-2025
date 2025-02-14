---
up:
  - "[[DAX-视觉计算]]"
related: 
created: 2025-02-08
tags: 
type: "[[Article]]"
finished: 2025-02-09
aliases:
  - introducing-visual-shape-for-visual-calculations-in-power-bi
---


[SQLBI原文](https://www.sqlbi.com/articles/introducing-visual-shape-for-visual-calculations-in-power-bi/)



# 模型度量值

> [!important]
>  矩阵是通过 返回的 **Flat Table 平面表** 查询 生成的
>  [[DAX-SummarizeColumns]] 的结果是平面的：所有行都处于同一级别，并且包含**原始值和小计的行之间没有差异**。Power BI 知道如何区分小计和常规行。但是，从 DAX 的角度来看，所有行都是相似的。

![image.png](https://s1.vika.cn/space/2025/02/09/dd912c2f6771405cb0b6a466fbc9a693)

```
EVALUATE
SUMMARIZECOLUMNS (
    ROLLUPADDISSUBTOTAL ( 'Product'[Brand], "IsGrandTotalRowTotal" ),
    ROLLUPADDISSUBTOTAL ( 'Date'[Year], "IsGrandTotalColumnTotal" ),
    "Sales_Amount", 'Sales'[Sales Amount]
)
```

![image.png](https://s1.vika.cn/space/2025/02/09/afd75e6dd48c45e6bb1e71f95064f685)


# 视觉计算计算过程

```
Growth =
VAR Curr = [Sales Amount]
VAR Prev = PREVIOUS ( [Sales Amount], COLUMNS )
VAR Result = DIVIDE ( Curr - Prev, Prev )
RETURN
    FORMAT ( Result, "0.00 %" )
```

![image.png|499](https://s1.vika.cn/space/2025/02/09/f17c84939cac4d85ac3a7cdb32fa37f5)

简化版查询

```
DEFINE
    COLUMN '__DS0VisualCalcs'[Growth] =
        (
            VAR Curr = [Sales Amount]
            VAR Prev =
                PREVIOUS ( [Sales Amount], COLUMNS )
            VAR Result =
                DIVIDE ( Curr - Prev, Prev )
            RETURN
                FORMAT ( Result, "0.00 %" )
        )
    VAR __DS0Core =
        SUMMARIZECOLUMNS (
            ROLLUPADDISSUBTOTAL ( 'Product'[Brand], "IsGrandTotalRowTotal" ),
            ROLLUPADDISSUBTOTAL ( 'Date'[Year], "IsGrandTotalColumnTotal" ),
            "Sales_Amount", 'Sales'[Sales Amount]
        )
    VAR __DS0VisualCalcsInput =
        SELECTCOLUMNS (
            KEEPFILTERS (
                SELECTCOLUMNS (
                    __DS0Core,
                    "Brand", 'Product'[Brand],
                    "IsGrandTotalRowTotal", [IsGrandTotalRowTotal],
                    "Year", 'Date'[Year],
                    "IsGrandTotalColumnTotal", [IsGrandTotalColumnTotal],
                    "Sales_Amount", [Sales_Amount]
                )
            ),
            "Brand", [Brand],
            "Year", [Year],
            "IsGrandTotalRowTotal", [IsGrandTotalRowTotal],
            "IsGrandTotalColumnTotal", [IsGrandTotalColumnTotal],
            "Sales Amount", [Sales_Amount]
        )
    TABLE '__DS0VisualCalcs' = __DS0VisualCalcsInput
        WITH VISUAL SHAPE
        AXIS ROWS
            GROUP [Brand]
                TOTAL [IsGrandTotalRowTotal]
            ORDER BY [Brand] ASC
        AXIS COLUMNS
            GROUP [Year]
                TOTAL [IsGrandTotalColumnTotal]
            ORDER BY [Year] ASC
        DENSIFY "IsDensifiedRow"
    VAR __DS0RemoveEmptyDensified =
        FILTER (
            KEEPFILTERS ( '__DS0VisualCalcs' ),
            OR (
                NOT ( '__DS0VisualCalcs'[IsDensifiedRow] ),
                NOT ( ISBLANK ( '__DS0VisualCalcs'[Growth] ) )
            )
        )
    VAR __DS0RemoveContextOnlyColumns =
        SELECTCOLUMNS (
            KEEPFILTERS ( __DS0RemoveEmptyDensified ),
            "'__DS0VisualCalcs'[Brand]", '__DS0VisualCalcs'[Brand],
            "'__DS0VisualCalcs'[Year]", '__DS0VisualCalcs'[Year],
            "'__DS0VisualCalcs'[IsGrandTotalRowTotal]",
                '__DS0VisualCalcs'[IsGrandTotalRowTotal],
            "'__DS0VisualCalcs'[IsGrandTotalColumnTotal]",
                '__DS0VisualCalcs'[IsGrandTotalColumnTotal],
            "'__DS0VisualCalcs'[Growth]", '__DS0VisualCalcs'[Growth],
            "'__DS0VisualCalcs'[IsDensifiedRow]", '__DS0VisualCalcs'[IsDensifiedRow]
        )
EVALUATE
    __DS0RemoveContextOnlyColumns  
    
```

The query contains a lot of information to process:  
查询包含大量要处理的信息：

- **DEFINE COLUMNS**.  可视化计算是使用 DEFINE COLUMNS 创建为查询列的。
- 基础查询与前面的矩阵相同（参见 `__Ds0Core`）
- 基础查询将经历几个处理步骤：
    - 重命名列
    - 添加 VISUAL SHAPE 和增密化过程(densification process)
    -  删除可视化计算中没有值的增密行
    - 删除用于计算但视觉对象不需要的列


# 复杂一点的案例

![image.png](https://s1.vika.cn/space/2025/02/09/e52f56970a534e8fbe00879cb750783e)


![image.png](https://s1.vika.cn/space/2025/02/09/12600f168a1849c2967817dfb566d667)

![image.png](https://s1.vika.cn/space/2025/02/09/cbadbb8952014c1d94ca93eb819fe049)

有两个字段的 Group 通常是有设定排序方式
# 本文最关注的 Visual Shape

```
TABLE '__DS0VisualCalcs' = __DS0VisualCalcsInput
    WITH VISUAL SHAPE
    AXIS ROWS
        GROUP [Brand]
            TOTAL [IsGrandTotalRowTotal]
        ORDER BY [Brand] ASC
    AXIS COLUMNS
        GROUP [Year]
            TOTAL [IsGrandTotalColumnTotal]
        ORDER BY [Year] ASC
    DENSIFY "IsDensifiedRow"
```


- ROWS 和 COLUMNS 是只能在视觉计算中使用的关键字。
- 因为模型度量可以添加到没有可视化计算的矩阵中，常规度量不能使用可视化视觉计算


 It is worth noting that the table with VISUAL SHAPE is not a variable; it is a query-defined table.
值得注意的是，具有 VISUAL SHAPE 的表不是变量;它是一个查询定义的表

- 视觉计算都是列 （这个列其实是`__DS0VisualCalcs` 这个 Flat Table 的列）
	- 这个 Flat Table 被定义了一些元数据
- 列不能被添加为变量
- 这些列可以引用 Rows 和 Columns

# 下一步

了解 VISUAL SHAPE 语法是了解如何计算可视化计算的第一步。接下来，了解由**轴定义的级别晶格**以及 [EXPAND](https://dax.guide/expand/?aff=sqlbi) 和 [COLLAPSE](https://dax.guide/collapse/?aff=sqlbi) 如何让开发人员在晶格中导航非常重要。