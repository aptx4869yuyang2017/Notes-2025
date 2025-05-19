---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH10 使用筛选上下文]]"
  - "[[SQLBI-在视觉计算中使用 Expand 和 Collapse]]"
created: 2025-02-06
tags:
  - domain/powerbi
---

# 需求1 月粒度数据不要求继续拆分通胀系数

![image.png](https://s1.vika.cn/space/2025/02/06/535211529bf54b8fb40bb93a6d017e39)


# 实现1


度量值 用到了 **HasOneValue**
```
User Selected Inflation = IF ( HASONEVALUE( 'Inflation Rate'[Inflation] ), VALUES ( 'Inflation Rate'[Inflation] ), 0 )
```

![image.png](https://s1.vika.cn/space/2025/02/06/38e8c65b5d5d459296e7a10353fd6e73)




度量值 用到了 **SelectedValue**

思路
- 找到报告最晚年份
- 找到当前筛选上下文年份
- 两个年份构建一个 年份列表
- ProductX 其实就是遍历年份 多少年就是多少次方
- 用 Max 做一下保护

```
Inflation Multiplier = 
VAR ReportingYear =
    YEAR ( CALCULATE ( MAX ( Sales[Order Date] ), ALL ( Sales ) ) )
VAR CurrentYear =
    SELECTEDVALUE ( 'Date'[Calendar Year Number] )
VAR Inflation = [User Selected Inflation]
VAR Years =
    FILTER (
        ALL ( 'Date'[Calendar Year Number] ),
        AND (
            'Date'[Calendar Year Number] >= CurrentYear,
            'Date'[Calendar Year Number] < ReportingYear
        )
    )
VAR Multiplier =
    MAX ( PRODUCTX ( Years, 1 + Inflation ), 1 )
RETURN
    Multiplier
```



```
Inflation Adjusted Sales = SUMX ( VALUES ( 'Date'[Calendar Year] ), [Sales Amount] * [Inflation Multiplier] )
```


# 需求2: 月粒度数据也需要拆分通胀系数


[[SQLBI-在视觉计算中使用 Expand 和 Collapse]]