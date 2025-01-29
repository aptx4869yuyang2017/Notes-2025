---
up:
  - "[[Data MOC]]"
related:
  - "[[DAX 权威指南(book)]]"
  - "[[Optimizing DAX 优化DAX(book)]]"
created: 2024-12-07
tags:
  - map
aliases:
  - PowerBI Performance
---

- RelatedTable vs Calculate
	- [[DAX-All & AllExcept#^f02df8]]
	- 涉及了三种写法，方案二 -> 方案三 
- RelatedTable vs CalculateTable
	- [[DAX-RelatedTable]]


# 语法糖

- SUMX vs SUM
- Calculate 的参数 [[DAX-Calculate#^e30627]]



# Calculate 的 筛选参数 到底应该怎么写？（不fancy）

- **单表单列**  `Sales[Net Price] >= 10 && Sales[Net Price] <= 100)`
- **单表多列** `Sales[Quantity] ** Sales[Net Price] >= 1000)`
- 多表多列

[[DAX-Calcualte-多条件筛选(21-03之后)]]
[[DAX-Calculate-多条件筛选-Performance]]


# 模型优化

- [[DAX-Case-关闭自动日期时间]]



 > [!important] Performance
> 所有自动获取的 performance 标签
> 
> ```dataview
> LIST
> FROM #domain/powerbi/performance 
> SORT file.cday desc
> ```
