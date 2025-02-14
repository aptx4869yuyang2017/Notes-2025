---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-设计模式(book)]]"
created: 2025-02-11
tags:
  - domain/powerbi
---

动态分组模式 **度量值对实体进行分类**。


# 需求 1

**你需要根据消费金额对客户进行分类**

![image.png](https://s1.vika.cn/space/2025/02/11/176f05ff933347c892606dd69a8629cc)


# 客户数统计


![image.png](https://s1.vika.cn/space/2025/02/11/fa2b9ae1f1c64a338f51434e1e1c7cb3)


```
# Seg. Customers = 
IF (
    HASONEVALUE ( 'Date'[Calendar Year] ),  -- Segmentation only over one year selected
    VAR CustomersInSegment =                -- Gets the customers in the current segment
        FILTER ( 
            ALLSELECTED ( Customer ),
            VAR SalesOfCustomer = [Sales Amount] -- Computes Sales Amount for one customer
            VAR SegmentForCustomer =             -- Retrieves the segment 
                FILTER (                         -- a customer belongs to
                    'Customer Segments',
                    NOT ISBLANK ( SalesOfCustomer )
                        && 'Customer Segments'[Min Sales] < SalesOfCustomer
                        && 'Customer Segments'[Max Sales] >= SalesOfCustomer
                )
            VAR IsCustomerInSegments = NOT ISEMPTY ( SegmentForCustomer )
            RETURN IsCustomerInSegments
        )
    VAR Result =
        CALCULATE (
            COUNTROWS ( Customer ),             -- Expression to compute
            KEEPFILTERS ( CustomersInSegment )  -- Applies filter for segmented customers 
        )
    RETURN Result
) 
```


# 统计销售额


![image.png](https://s1.vika.cn/space/2025/02/11/019452b7a015433dbda68ebf5c1df2d8)


![image.png|426](https://s1.vika.cn/space/2025/02/11/4c2ee818a2b04f7babf05fbc2b3df696)
![image.png|424](https://s1.vika.cn/space/2025/02/11/6c0665164e5540b9bb231c7efa21d3c3)

```
Sales Seg. Customers = 
SUMX (
    VALUES ( 'Date'[Calendar Year] ),       -- 在每个所选年份上重复计算分类
    VAR CustomersInSegment =                -- 获取当前分类下的客户 
        FILTER ( 
            ALLSELECTED ( Customer ),
            VAR SalesOfCustomer = [Sales Amount] -- 计算单个客户销售额
            VAR SegmentForCustomer =             -- 获得客户所属分类
                FILTER (                         
                    'Customer Segments',
                    NOT ISBLANK ( SalesOfCustomer )
                        && 'Customer Segments'[Min Sales] < SalesOfCustomer
                        && 'Customer Segments'[Max Sales] >= SalesOfCustomer
                )
            VAR IsCustomerInSegments = NOT ISEMPTY ( SegmentForCustomer )
            RETURN IsCustomerInSegments
        )
    VAR Result =
        CALCULATE (
            [Sales Amount],                     -- 需要计算的表达式
            KEEPFILTERS ( CustomersInSegment )  -- 对分类的客户应用筛选
        )
    RETURN Result
)

```

- 按年度区分 客户 等级 所以是最外层迭代
	- CustomersInSegment 只保留 特定 Segment 的 Customer
	- 在 CustomersInSegment 环境下 计算 Sales Amount



# 需求2 根据客户巅峰消费年份分类

![image.png](https://s1.vika.cn/space/2025/02/11/47bf19e10dd84b61bdcf83536194ef17)

定义 最大的年销售额


![image.png](https://s1.vika.cn/space/2025/02/11/e418f8b78c8142478eb004d75d134ca4)


- 遍历用户，根据最大年销售额，保留 具体 Segments 下的所有用户
- 根据客户list ，计算 Sales Amount

