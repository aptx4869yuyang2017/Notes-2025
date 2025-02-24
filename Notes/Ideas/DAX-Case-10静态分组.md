---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-设计模式(book)]]"
created: 2025-02-11
tags:
  - domain/powerbi
---

# 静态分组


![image.png](https://s1.vika.cn/space/2025/02/11/dab09112546d45c9946e3a99f4878e8f)


## 1.1 构建表


```
Price Ranges = 
DATATABLE(
    "PriceRangeKey", INTEGER,
    "Price Range", STRING,
    "Min Price", CURRENCY,
    "Max Price", CURRENCY,
    {
        { 1, "VERY LOW", 0, 100 },
        { 2, "LOW", 100, 300 },
        { 3, "MEDIUM", 300, 600 },
        { 4, "HIGH", 600, 1500 },
        { 5, "VERY HIGH", 1500, 999999999 }
    }
)

```
![image.png](https://s1.vika.cn/space/2025/02/11/9e9b906fc6d942518d9730f8db049fe5)

## 1.2 构建键值 


```
PriceRangeKey = 
VAR CurrentPrice = Sales[Net Price]
VAR FilterSegment =
    FILTER (
        'Price Ranges',
        AND (
            'Price Ranges'[Min Price] < CurrentPrice,
            'Price Ranges'[Max Price] >= CurrentPrice
        )
    )
VAR FilteredPriceRangeKey =
    CALCULATETABLE (
        DISTINCT ( 'Price Ranges'[PriceRangeKey] ),
        FilterSegment
    )
VAR Result =
    IF (
        COUNTROWS ( FilteredPriceRangeKey ) = 1,
        FilteredPriceRangeKey,
        
        -- 下一行在计算列中引发了更具体的错误 
		-- 您可以用 BLANK() 替换 ERROR，以便忽略匹配多个区段的价格， 
		-- 但请记住，这样做会隐藏报告中的可能错误
		
        ERROR ( "Overlapping ranges in Price Ranges table" )
    )
RETURN
    Result
```


# 根据类别 静态分组


## 构造表

![image.png](https://s1.vika.cn/space/2025/02/11/f6a55286ee184492806d9fbc0a96c23b)


## 计算列

![image.png](https://s1.vika.cn/space/2025/02/11/97ee5c6f07df4330a75e1c1c2ae47e0d)


# 性能优化


> [!important]
>  静态分组模式要求在 Sales 表中创建一个计算列。列所占的内存很小，因为它包含的值基 本相同。但是，在非常大的表上，列的大小可能开始增大，并且你会面临另一个问题:每当数 据刷新时，该列都要被重新计算。在可能要进行分区的数十亿行的表中，每刷新一个分区，该列在整个表中都要重算。这会减慢每次刷新操作的速度。

## 原始配置表

![image.png](https://s1.vika.cn/space/2025/02/11/54e19fa6a8734875bbbca49397cf187e)

## 展示出来的配置表

```
Price Ranges = 
GENERATE (
    'Price Ranges Configuration',
    FILTER (
        ALLNOBLANKROW ( Sales[Net Price] ),
        AND (
            Sales[Net Price] > 'Price Ranges Configuration'[Min Price],
            Sales[Net Price] <= 'Price Ranges Configuration'[Max Price]
        )
    )
)
```

# 新的模型

![image.png](https://s1.vika.cn/space/2025/02/11/dd0cf4124c924441996a13120a4c8246)


