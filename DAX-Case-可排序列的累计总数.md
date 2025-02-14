---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-设计模式(book)]]"
created: 2025-02-11
tags:
  - domain/powerbi
---

# 需求

![image.png|540](https://s1.vika.cn/space/2025/02/11/3a26d54f374049b8a9e0f9bbcac9686f)


# Step 1 构造静态范围表


![image.png|629](https://s1.vika.cn/space/2025/02/11/9bef7bee1f8442b2b81d51133a35dc05)


表
```
Customer classes = 
VAR CustomerClasses =
    DATATABLE (
        "Customer class number", INTEGER,
        "Customer class", STRING,
        "Min Sales", CURRENCY,
        {
            { 1, "Silver", 0 },
            { 2, "Gold", 5000 },
            { 3, "Platinum", 50000 },
            { 4, "Titanium", 150000 }
        }
    )
VAR MaxSalesEver =
    CALCULATE (
        [Sales Amount],
        REMOVEFILTERS ()
    )
RETURN
    ADDCOLUMNS (
        CustomerClasses,
        "Max Sales",
        VAR CurrMinSales = [Min Sales]
        RETURN
            COALESCE (
                MINX (
                    FILTER (
                        CustomerClasses,
                        [Min Sales] > CurrMinSales
                    ),
                    [Min Sales]
                ),
                MaxSalesEver
            )
    )
```

- 找大于行数的，最小数值
- Coalesce ：空缺填写整体 [Sales Amount]

# 度量值

```
Sales Amount RT Class = 
VAR LastVisibleClass =
    MAX ( Customer[Customer Class Number] )
VAR ClassesToSum =
    FILTER ( 
        ALLSELECTED ( 
            Customer[Customer Class], 
            Customer[Customer Class Number] 
        ),
        Customer[Customer Class Number] <= LastVisibleClass
    )
VAR Result =
    CALCULATE ( 
        [Sales Amount], 
        ClassesToSum    
   )
RETURN
    Result
```

