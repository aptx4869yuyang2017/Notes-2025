---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH16 DAX高级计算]]"
created: 2025-02-09
tags:
  - domain/powerbi
---
# 需求：只有门店在选定年份都营业才会返回结果

![image.png](https://s1.vika.cn/space/2025/02/09/84bcc9d42c4841cf8522cbe0990970ed)


![image.png](https://s1.vika.cn/space/2025/02/09/1dbd88bd0f7747ffa387f8dd85b0b9e3)


# 方案一： 使用独立的状态表 StoresStatus

## 独立出来状态表 StoresStatus

![image.png](https://s1.vika.cn/space/2025/02/09/bbafcb08f0f14455bab46b753547afd4)

![image.png](https://s1.vika.cn/space/2025/02/09/72eb5eee4e364f838f12ca0ff033417a)

```
StoresStatus = 
VAR OpenStores =
    SUMMARIZE (
        Receipts,
        'date'[Calendar Year Number],
        'Product Category'[Category],
        [StoreKey]
    )
VAR AllStores =
    CALCULATETABLE (
        CROSSJOIN (
            CROSSJOIN (
                DISTINCT ( 'date'[Calendar Year Number] ),
                DISTINCT ( 'Product Category'[Category] )
            ),
            ALLNOBLANKROW ( Store[StoreKey] )
        ),
        FILTER (
            ALLNOBLANKROW ( 'Date'[Calendar Year Number] ),
            'Date'[Calendar Year Number] IN { 2007, 2008, 2009 }
        )
    )
RETURN
    UNION (
        ADDCOLUMNS ( OpenStores, "Status", "Open" ),
        ADDCOLUMNS ( EXCEPT ( AllStores, OpenStores ), "Status", "Closed" )
    )
```

- 使用 [[DAX-CrossJoin]] 找到 Year - StoreKey - Product Category 的所有组合
- 使用 [[DAX-Summarize]] 找到 Receipts 中存在的 Year - StoreKey - Product Category 组合
- Union 两部分
	- AddColumn 增加标签信息
	- [[DAX-Except]] 取差集

## 模型


![image.png](https://s1.vika.cn/space/2025/02/09/6736a055c22d427c9dddff514b5a8d2e)

- 注意 Date StoresStatus 是有限关系


## 确定哪些部门在选定年份营业


![image.png|447](https://s1.vika.cn/space/2025/02/09/ebd82c46ee014ff4b15167b852dd1384)

- 利用了 [[DAX-HasOneValue & SelectedValue | SelectedValue]] 来保证 只有 "Open" 一个状态
- 


![image.png|437](https://s1.vika.cn/space/2025/02/09/8823c4bf3a844d219dc2a225bf8acc08)


- 计算一个包含 [[DAX-Filter]] 的表
	-  The ability to compute a table containing a filter 
- 用作后续计算的约束条件 
	- then use it to restrict the calculation is the foundation of several advanced calculations in DAX.

# 方案二：不使用状态表


![image.png](https://s1.vika.cn/space/2025/02/09/83827643f1524cf89bf4374793314a5b)
![image.png](https://s1.vika.cn/space/2025/02/09/5bd15adfcce04c1098665e2bd94b0a6c)

- 检测选中的年份数量 是不是和 Receipts 中的年份数量一致
