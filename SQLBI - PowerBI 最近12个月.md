---
up:
  - "[[PowerBI Tricks]]"
related:
  - "[[SQLBI]]"
created: 2025-09-13
tags:
  - domain/powerbi
---

> [!important] X轴 时间
> **要用 Previous Date**


![image.png](https://s1.vika.cn/space/2025/09/13/6583b486c9214b599b6abac664392d9a)
- Previous Date

![image.png](https://s1.vika.cn/space/2025/09/13/c1fff0e36c564dd3b21a4da602a54e9f)

![image.png](https://s1.vika.cn/space/2025/09/13/26dce4e46e5447d9b41555cd26cbefbb)


```
Previous 6 Months =
--  This calculation item works together with the Previous Date table to show
--  6 months back from the currently selected date in the Date table
--
VAR NumOfMonths = -6
VAR ReferenceDate = MAX ( 'Date'[Date] )
VAR PreviousDates = DATESINPERIOD ( 'Previous Date'[Date], ReferenceDate, NumOfMonths, MONTH )
VAR Result =
    CALCULATE (
        SELECTEDMEASURE (),
        REMOVEFILTERS ( 'Date' ),
        KEEPFILTERS ( PreviousDates ),
        USERELATIONSHIP ( 'Previous Date'[Date], 'Date'[Date] )
    )
RETURN Result
```


![image.png](https://s1.vika.cn/space/2025/09/13/b80e1cdf872f4cd98be827c1ccf71ebe)


```
Current Year = --
--  This calculation item works together with the Previous Date table to show
--  6 months back from the currently selected date in the Date table
--
VAR NumOfMonths = -12
VAR ReferenceDate = MAXX ( endofyear('Date'[Date]), 'Date'[Date] )
VAR PreviousDates = DATESINPERIOD ( 'Previous Date'[Date], ReferenceDate, NumOfMonths, MONTH )
VAR Result =
    CALCULATE (
        SELECTEDMEASURE (),
        REMOVEFILTERS ( 'Date' ),
        KEEPFILTERS ( PreviousDates ),
        USERELATIONSHIP ( 'Previous Date'[Date], 'Date'[Date] )
    )
RETURN Result
```