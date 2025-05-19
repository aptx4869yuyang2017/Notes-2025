---
up:
  - "[[DAX-视觉计算]]"
related: 
created: 2025-02-09
tags: 
type: "[[Article]]"
finished: 
aliases: 
---
[Using EXPAND and COLLAPSE in visual calculations - SQLBI](https://www.sqlbi.com/articles/using-expand-and-collapse-in-visual-calculations/)

# 视觉计算版本




## 通胀系数的存储


![image.png](https://s1.vika.cn/space/2025/02/09/4a6a48f708e242c8aa437da5884879eb)


因为视觉计算无法访问到模型表，所以使用 Switch 存储信息


## 计算每月调整


```
Cumulative Adjustment = 
VAR Months =
    CALCULATETABLE (
        CALCULATETABLE (
            ROWS,
            EXPAND ( [Year-Month Month] )
        ),
        COLLAPSEALL ( ROWS )
    )
VAR CumulativeAdjustment = 
    CALCULATE ( 
        PRODUCTX ( 
            WINDOW ( 1, ABS, -1, REL, Months, ORDERBY( [Year_Month_Number], DESC ) ),
            POWER ( [Yearly Adjustment], 1/12 )
        ),
        COLLAPSE ( [Year-Month Date] )
    )
VAR Result = 
    IF ( 
        ISATLEVEL([Year-Month Month] ), 
        COALESCE ( CumulativeAdjustment, 1 ) 
    )
RETURN
    Result
```

### Rows 返回行集

**月份包含在虚拟表中，我们可以通过 ROWS 访问虚拟表。在可视化计算中，ROWS 返回当前视觉上下文级别的行集**

![image.png|340](https://s1.vika.cn/space/2025/02/09/5cc46f089f22446eb5c9c8f17bbbd4da)

如果只有四年就是四行

![image.png|460](https://s1.vika.cn/space/2025/02/09/09a631c4c91c44da82afe2649ad2791f)

当只有两年 15个月，Rows 返回15行







The months are contained in the virtual table, and we can access the virtual table through ROWS. ROWS, in a visual calculation, returns the set of rows at the current visual context level.



理解这句话
**该算法需要迭代当前月份之后的所有月份**


比如 计算2009-10的调整系数，当前时间是 2010-02
那么 应该是  **2009-11** x **2009-12** x **2010-01** x **2010-02**



# 模型度量值版本

- [[DAX-AddColumns & SelectColumns|SelectColumns]] 存年通胀率，改名字
- 遍历 Sales 找到最晚的**年月信息**
- 把年粒度的通胀率拓展到 月粒度
	- [[DAX-Generate & GenerateAll|Generate]] 起到笛卡尔积的作用，还是有一定筛选功能，拓展出 月粒度
	- 改名字，增加月通胀率
	- 限制数据到最新年月
- 两次遍历 MonthlyAdjustment 算每个月的 累计通胀率
	- 遍历1: 遍历月
	- 遍历2: 当前月 - 最新月 这个范围 ProductX
- 结合累计通胀率计算
	- 使用 [[DAX-NaturalLeftOuterJoin]] 存在数据沿袭的情况下关联


```
VAR YearlyAdjustment =
    SELECTCOLUMNS (
        { ( 2017, 2.13 ), ( 2018, 2.44 ), ( 2019, 1.81 ), ( 2020, 1.23 ) },
        "Year", [Value1],
        "Yearly Adjustment", [Value2] / 100 + 1
    )
--
--  找到最后一个有销售记录的可见年月
--  以便确定用于计算通货膨胀的日期。
--
VAR LastVisibleYearMonth =
    CALCULATE (
        MAXX (
            SUMMARIZE ( Sales, 'Date'[Year Month Number] ),
            'Date'[Year Month Number]
        ),
        ALLSELECTED ()
    )
--
--  将年度通胀转换为月度水平 使用 Generate
--  去除在 LastVisibleYearMonth 之后的时期
--  并添加 Year Month Number 列，以便后续与销售数据连接。
--
VAR MonthlyAdjustment =
    FILTER (
        SELECTCOLUMNS (
            GENERATE (
                YearlyAdjustment,
                VAR CurrentYear = [Year]
                RETURN
                CALCULATETABLE (
                    VALUES ( 'Date'[Year Month Number] ),
                    REMOVEFILTERS ( 'Date' ),
                    'Date'[Year] = CurrentYear
                )
            ),
            "Year Month Number", 'Date'[Year Month Number],
            "Monthly Adjustment", POWER ( [Yearly Adjustment], 1 / 12 )
        ),
        [Year Month Number] <= LastVisibleYearMonth
    )
--
--  计算每个月需要应用的累计通货膨胀，以调整销售。
--
VAR CumulativeAdjustment =
    ADDCOLUMNS (
        MonthlyAdjustment,
        "Cumulative Adjustment",
            VAR CurrentYearMonth = [Year Month Number]
            RETURN
                COALESCE (
                    PRODUCTX (
                        FILTER ( MonthlyAdjustment, [Year Month Number] > CurrentYearMonth ),
                        [Monthly Adjustment]
                    ),
                    1
                )
    )
--
--  按年份月份编号计算销售额，以便稍后与累计调整进行连接
--
VAR SalesByMonth =
    SELECTCOLUMNS (
        SUMMARIZE ( Sales, 'Date'[Year Month Number] ),
        "Monthly Sales", [Sales Amount],
        "Year Month Number", 'Date'[Year Month Number]
    )
--
--  按月调整销售额，结合累计通货膨胀进行计算
--
VAR SalesAdjusted =
    ADDCOLUMNS (
        NATURALLEFTOUTERJOIN ( SalesByMonth, CumulativeAdjustment ),
        "Adjusted Sales", [Monthly Sales] * [Cumulative Adjustment]
    )
VAR Result = SUMX ( SalesAdjusted, [Adjusted Sales] )
RETURN
    Result
```


