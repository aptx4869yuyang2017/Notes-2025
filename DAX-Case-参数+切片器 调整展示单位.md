---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-设计模式(book)]]"
created: 2025-02-11
tags:
  - domain/powerbi
---
![image.png](https://s1.vika.cn/space/2025/02/11/9b4e8dfd1bb64d3893cf287dae4af25a)

# 构造参数表

```
Scale = 
DATATABLE (
    "Scale", STRING,
    "Denominator", INTEGER,
    {
        { "Units", 1 },
        { "Thousands", 1000 },
        { "Millions", 1000000 }
    }
)
```


# 构造度量值

```
Sales Amount = 
VAR RealValue =
    SUMX (
        Sales,
        Sales[Quantity] * Sales[Net Price]
    )
VAR Denominator =
    SELECTEDVALUE (
        Scale[Denominator],
        1
    )
VAR Result =
    DIVIDE (
        RealValue,
        Denominator
    )
RETURN
    Result
```

- SelectedValue 找选中值
- 安全除法


