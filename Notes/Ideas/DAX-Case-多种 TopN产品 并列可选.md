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

![image.png](https://s1.vika.cn/space/2025/02/11/d0658db3661b472ea7b8f501b3cf7e75)



# 构造表


```
TopN Filter = 
ADDCOLUMNS (
    SELECTCOLUMNS ( 
        { 0, 1, 5, 10, 20, 50 }, 
        "TopN", [Value] 
    ),
    "TopN Products", IF (
        [TopN] = 0,
        "All",
        "Top " & [TopN]
    )
)
```



# 度量值


```
Top Sales = 
VAR TopNvalue =
    SELECTEDVALUE ( 'TopN Filter'[TopN], 0 )
VAR TopProducts =
    TOPN ( TopNvalue, 'Product', [Sales Amount] )
VAR AllSales = [Sales Amount]
VAR TopSales =
    CALCULATE ( [Sales Amount], KEEPFILTERS ( TopProducts ) )
VAR Result =
    IF ( TopNvalue = 0, AllSales, TopSales )
RETURN
    Result
```


- 到底 TopN 有哪些 
	- **注意这里 TopN 值可以多选，但是因为 表格中列是 TopN 所以 SelectedValue 可以保证只有一个值**
	- 利用 [[DAX-TOPN]] 函数保留特定的 产品