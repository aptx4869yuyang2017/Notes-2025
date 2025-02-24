---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-设计模式(book)]]"
created: 2025-02-11
tags:
  - domain/powerbi
---
# 静态 ABC


![image.png](https://s1.vika.cn/space/2025/02/11/7eb9633eeb524e4f83b7a890aaed610b)


# ABC 快照


**ABC by Year** 表

```
ABC by Year = 
VAR ProductsByYear =
    SUMMARIZE (
        Sales,
        'Product'[ProductKey],
        'Date'[Calendar Year]
    )
VAR SaleByYearProduct =
    ADDCOLUMNS (
        ProductsByYear,
        "@ProdSales", [Sales Amount],
        "@YearlySales", CALCULATE (
            [Sales Amount],
            ALL ( 'Product' )
        )
    )
VAR CumulatedSalesByYearProduct =
    ADDCOLUMNS (
        SaleByYearProduct,
        "@CumulatedSales",
        VAR CurrentSales = [@ProdSales]
        VAR CurrentYear = 'Date'[Calendar Year]
        VAR CumulatedSalesWithinYear =
            FILTER (
                SaleByYearProduct,
                AND (
                    'Date'[Calendar Year] = CurrentYear,
                    [@ProdSales] >= CurrentSales
                )
            )
        RETURN
            SUMX (
                CumulatedSalesWithinYear, 
                [@ProdSales]
            )
    )
VAR CumulatedPctByYearProduct =
    ADDCOLUMNS (
        CumulatedSalesByYearProduct,
        "@CumulatedPct", DIVIDE (
            [@CumulatedSales],
            [@YearlySales]
        )
    )
VAR ClassByYearProduct =
    ADDCOLUMNS (
        CumulatedPctByYearProduct,
        "@AbcClass", SWITCH (
            TRUE,
            [@CumulatedPct] <= 0.7, "A",
            [@CumulatedPct] <= 0.9, "B",
            "C"
        )
    )
VAR Result =
    SELECTCOLUMNS (
        ClassByYearProduct,
        "ProductKey", 'Product'[ProductKey],
        "Calendar Year", 'Date'[Calendar Year],
        "ABC Class", [@AbcClass]
    )
RETURN
    Result
```



![image.png](https://s1.vika.cn/space/2025/02/11/850b3b2ff88a4baa94e219d5a1256347)


```
ABC Sales Amount = 
VAR RemapFilterAbc =
    TREATAS (
        'ABC by Year',            -- Remap the columns of ABC by Year 
        'Product'[ProductKey],    -- so that only the specific
        'Date'[Calendar Year],    -- combinations of product and year
        'ABC by Year'[ABC Class]  -- are included in the filter context
    )
VAR Result =
    CALCULATE (
        [Sales Amount],
        KEEPFILTERS ( RemapFilterAbc )
    )
RETURN
    Result
```

![image.png](https://s1.vika.cn/space/2025/02/11/0122e7cb87e3495dabd8e46444a85f6c)

- 修改数据沿袭
- 直接利用 筛选上下文中的信息 作为 计算的条件


# 动态ABC


## 需求

![image.png](https://s1.vika.cn/space/2025/02/11/2f2fe6ccdb4a44448be1f907708ef42f)

- 根据 Category 确定 Product 范围
- 提前确定 ABC 的边界 **ABC Class**

## 边界表

![image.png](https://s1.vika.cn/space/2025/02/11/c4aceda84ccc4c9397d61f9379ad6051)

## Sales 计算



```
ABC Sales Amount = 
-- Customization required for different models:
--   'Product'         --> Table with the entity to segment (customers, products, ...)
--   [Sales Amount]    --> Measure to use for ABC segmentation
--
VAR SalesByProduct =
    ADDCOLUMNS (
        ALLSELECTED ( 'Product' ),
        "@ProdSales", [Sales Amount]
    )
VAR AllSales =
    CALCULATE (
        [Sales Amount],
        ALLSELECTED ( 'Product' )
    )
VAR CumulatedPctByProduct =
    ADDCOLUMNS (
        SalesByProduct,
        "@CumulatedPct",
        VAR CurrentSalesAmt = [@ProdSales]
        VAR CumulatedSales =
            FILTER (
                SalesByProduct,
                [@ProdSales] >= CurrentSalesAmt
            )
        VAR CumulatedSalesAmount =
            SUMX (
                CumulatedSales,
                [@ProdSales]
            )
        RETURN
            DIVIDE (
                CumulatedSalesAmount,
                AllSales
            )
    )
VAR ProductsInClass =
    FILTER (
        CROSSJOIN (
            CumulatedPctByProduct,
            'ABC Classes'
        ),
        AND (
            [@CumulatedPct] > 'ABC Classes'[Lower Boundary],
            [@CumulatedPct] <= 'ABC Classes'[Upper Boundary]
        )
    )
VAR Result =
    CALCULATE (             -- The pattern is the same for every measure, just
        [Sales Amount],     -- change this measure reference for other measures
        KEEPFILTERS ( ProductsInClass )
    )
RETURN
    Result
```





- 遍历所有选中 Product 计算 Sales 
- 算所有产品 Total Sales 
- 继续遍历产品，获取 单个产品占比
- [[DAX-CrossJoin]] ABC Class 表 
	- 通过 筛选，做了 占比 - ABC Class 的匹配
- 通过 Calculate 作为参数计算 注意使用 [[DAX-KeepFilters]]

## 产品数计算

```

# Products = 
VAR ProdSales =
    ADDCOLUMNS (
        ALLSELECTED ( 'Product' ),
        "@Sales", [Sales Amount]
    )
VAR AllSales =
    CALCULATE (
        [Sales Amount],
        ALLSELECTED ( 'Product' )
    )
VAR ProdSalesPerc =
    ADDCOLUMNS (
        ProdSales,
        "@AggSales%",
        VAR CurrentSalesAmt = [@Sales]
        VAR CumulatedSales =
            SUMX (
                FILTER (
                    ProdSales,
                    [@Sales] >= CurrentSalesAmt
                ),
                [@Sales]
            )
        RETURN
            DIVIDE (
                CumulatedSales,
                AllSales
            )
    )
VAR ProductsInClass =
    FILTER (
        CROSSJOIN (
            ProdSalesPerc,
            'ABC Classes'
        ),
        AND (
            [@AggSales%] > 'ABC Classes'[Lower Boundary],
            [@AggSales%] <= 'ABC Classes'[Upper Boundary]
        )
    )
VAR Result =
    CALCULATE (
        COUNTROWS ( 'Product' ),
        KEEPFILTERS ( ProductsInClass )
    )
RETURN
    Result
```


# 展示 ABC 分组


![image.png](https://s1.vika.cn/space/2025/02/11/bb2e04faa26e4a09a821642c4031b8cc)


```
ABC Class = 
-- Customization required for different models:
--   'Product'         --> Table with the entity to segment (customers, products, ...)
--   [Sales Amount]    --> Measure to use for ABC segmentation
--
IF (
    HASONEVALUE ( 'Product'[ProductKey] ),
    VAR SalesByProduct =
        ADDCOLUMNS (
            ALLSELECTED ( 'Product' ),
            "@ProdSales", [Sales Amount]
        )
    VAR AllSales =
        CALCULATE (
            [Sales Amount],
            ALLSELECTED ( 'Product' )
        )
    VAR CurrentSalesAmt = [Sales Amount]
    VAR CumulatedSales =
        FILTER (
            SalesByProduct,
            [@ProdSales] >= CurrentSalesAmt
        )
    VAR CumulatedSalesAmount =
        SUMX (
            CumulatedSales,
            [@ProdSales]
        )
    VAR CurrentCumulatedPct =
        DIVIDE (
            CumulatedSalesAmount,
            AllSales
        )
    VAR Result =
        SWITCH (
            TRUE,
            ISBLANK ( CurrentCumulatedPct ), BLANK (),
            CurrentCumulatedPct <= 0.7, "A",
            CurrentCumulatedPct <= 0.9, "B",
            "C"
        )
    RETURN
        Result
)
```