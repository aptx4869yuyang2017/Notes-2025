---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-设计模式(book)]]"
created: 2025-02-11
tags:
  - domain/powerbi
---
# 场景1 简单累计



```
Sales Amount RT = 
VAR LastVisibleDate = MAX ( 'Date'[Date] )
VAR FirstVisibleDate = MIN ( 'Date'[Date] )
VAR LastDateWithSales = CALCULATE ( MAX ( 'Sales'[Order Date] ), REMOVEFILTERS () )
VAR Result = 
    IF ( 
        FirstVisibleDate <= LastDateWithSales, -- 第一可见 <= 全集最晚
        CALCULATE (
            [Sales Amount],
            'Date'[Date] <= LastVisibleDate -- 最晚可见 合计
        )
    )
RETURN
    Result
```

# 场景2 有额外的筛选

模型度量版本

```
RT Weekdays = 
VAR LastVisibleDate = MAX ( 'Date'[Date] )
VAR FirstVisibleDate = MIN ( 'Date'[Date] )
VAR LastDateWithSales = CALCULATE ( MAX ( 'Sales'[Order Date] ), REMOVEFILTERS () )
VAR Result = 
    IF ( 
        FirstVisibleDate <= LastDateWithSales,
        CALCULATE (
            [Sales Amount],
            'Date'[Date] <= LastVisibleDate,
            VALUES ( 'Date'[Day of Week] )
        )
    )
RETURN
    Result
```

视觉计算版本

```
Sales Amount RT Visual = RUNNINGSUM([Sales Amount])
```


![image.png](https://s1.vika.cn/space/2025/02/11/23a4bf64cf3a4579861557a42697b1bd)

