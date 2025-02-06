---
up:
  - "[[DAX-Calculate]]"
related:
  - "[[PowerBI 性能 MOC|PowerBI Performance]]"
created: 2025-01-28
tags:
  - domain/powerbi
---
[[DAX-Calcualte-多条件筛选(21-03之后)]]

- 单表单列  `Sales[Net Price] >= 10 && Sales[Net Price] <= 100)`
- 单表多列 `Sales[Quantity] ** Sales[Net Price] >= 1000)` **版本更新后支持，有两种写法，这次重点测试这两种写法的性能差异**
- 多表多列 只能使用 CrossJoin



> [!important]
> 1 能用 All 写法就用 All 写法，CrossJoin 有时候会性能极差
> 2 必须用 CrossJoin 的跨表场景 注意关联列的 Cardinality


```
DEFINE 

measure Sales[Sales-CROSSJOIN] =
CALCULATE(
    [Sales Amount],
    FILTER(
        CROSSJOIN (
            ALL ( 'Product'[Color] ),
            ALL ( 'Product'[Brand] )
        ),
        'Product'[Color] = "Red" || 'Product'[Brand] = "Contoso"
    )
)

measure Sales[Sales-All]=
CALCULATE (
    [Sales Amount],
    FILTER (
        ALL ( 'Product'[Color], 'Product'[Brand] ),
        'Product'[Color] = "Red" || 'Product'[Brand] = "Contoso"
    )
)

EVALUATE
SUMMARIZECOLUMNS('Date'[Year], "sales",'Sales'[Sales-All])
```

![image.png](https://s1.vika.cn/space/2025/01/28/d008a704f81c4bdfb5cb3e91902d154d)


![image.png](https://s1.vika.cn/space/2025/01/28/2be7dba1446a420f88f2ccd904a6cc61)


问题的关键在于
- 两次扫描是不是比一次扫描慢
- 同时也要看 两次扫描之后的 CrossJoin 也会有性能损耗，这里需要注意 FE 执行时间


---

# 使用 Customer 作为条件


```
DEFINE 

measure Sales[Sales-CROSSJOIN] =
CALCULATE(
    [Sales Amount],
    FILTER(
        CROSSJOIN (
            ALL ( 'Customer'[Name] ),
            ALL ( 'Customer'[City] )
        ),
        'Customer'[Name] = "Aaldert Olthoff" || 'Customer'[City] = "Landsmeer"
    )
)

measure Sales[Sales-All]=
CALCULATE (
    [Sales Amount],
    FILTER (
        ALL ( 'Customer'[Name], 'Customer'[City] ),
        'Customer'[Name] = "Aaldert Olthoff" || 'Customer'[City] = "Landsmeer"
    )
)

EVALUATE
SUMMARIZECOLUMNS('Date'[Year], "sales",'Sales'[Sales-CROSSJOIN])
```


![image.png](https://s1.vika.cn/space/2025/01/28/161943271b7a44a783b5aa9233e03e87)
直接内存不足了

![image.png](https://s1.vika.cn/space/2025/01/28/54e38d7251da411dabd32b43baa26885)
