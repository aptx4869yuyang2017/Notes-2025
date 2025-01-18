---
up:
  - "[[Optimizing DAX 优化DAX(book)]]"
related: 
year: 
created: 2024-08-25
tags: 
type: "[[Chapter]]"
ch: "09"
finished: 2024-08-25
aliases:
---
# 1 优化 datacache 使用


# 2 最佳产品的销售

案例：L03

![bf3ac66e2ae44b2494d729bd01212cdd|556](https://s1.vika.cn/space/2024/08/30/bf3ac66e2ae44b2494d729bd01212cdd)


![c4bc93ff76f443b88caa2df634585672|321](https://s1.vika.cn/space/2024/08/30/c4bc93ff76f443b88caa2df634585672)


![17b744af3fc546e4addf9241a47614e4|553](https://s1.vika.cn/space/2024/08/30/17b744af3fc546e4addf9241a47614e4)
![394a1f35b5d34618b8976c37b96509de|550](https://s1.vika.cn/space/2024/08/30/394a1f35b5d34618b8976c37b96509de)

**想法A**
- 不要重复的查询 SE，当一次查询已经有了可以得出结果的数据，那就不要再重复查询
- 我们可以避免按产品键（`Product[ProductKey]`）分组，这样可以避免在 VertiPaq 查询中进行连接操作，而是直接使用销售表中的产品键（`Sales[ProductKey]`）。
	- 这个优化效果不明显，因为SE还是挺快的


```
DEFINE
    MEASURE Sales[Sales of best products] =
        VAR ProductAndSales =
            ADDCOLUMNS (
                SUMMARIZE ( Sales, Sales[ProductKey] ),
                "@Sales", [Sales Amount]
            )
        VAR AvgSales =
            AVERAGEX ( ProductAndSales, [@Sales] )
        RETURN
            SUMX ( FILTER ( ProductAndSales, [@Sales] >= AvgSales ), [@Sales] )

EVALUATE
SUMMARIZECOLUMNS (
    Customer[Country],
    "Sales of best products", [Sales of best products]
)
```


**想法B**

- SE 查询的时候，扫描的表不同，性能也有差异

```
DEFINE
    MEASURE Sales[Sales of best products] =
        VAR ProductAndSales =
            ADDCOLUMNS (
                DISTINCT ( 'Product'[ProductKey] ),
                "@Sales", [Sales Amount]
            )
        VAR AvgSales =
            AVERAGEX ( ProductAndSales, [@Sales] )
        RETURN
            SUMX ( FILTER ( ProductAndSales, [@Sales] >= AvgSales ), [@Sales] )

EVALUATE
SUMMARIZECOLUMNS (
    Customer[Country],
    "Sales of best products", [Sales of best products]
)
```


# 3 Running total of sales and ABC analysis






# 4 Year-over-year customer growth as a percentage