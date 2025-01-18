---
created: ""
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "13"
---
## 基础语法

> [!note] 基础语法
> - define
> - measure
> - evaluate
> - order


## 常用函数

- Summarize
- SummarizeColumns
	- Ignore 可以带上空行
- TopN
- Generate / GenerateAll
	- 使用第一个表 对第二个表进行筛选
	- GenerateAll 不会跳过没有结果的空行
- IsOnOrAfter
	- 翻页，使用维度定位
- AddMissingItems
- GroupBy
	- 
- NaturalInnerJoin / NaturalLeftOuterJoin
	- 没有关系的 关联
	- 比如自己增加点排序表
- SubsituteWithIndex
	- 二维表的底层实现
- Sample



## 自动匹配

- SummarizeColumns
	- 来自一个表的列会进行 **自动匹配**，只展示已有组合
	- 来自不同表的列的不会进行 **自动匹配**， 但是如果新增列为**空**，会进行值的删除操作
	- AddMissingItems 只是会还原删除空值的 行，并不会逆转 **自动匹配** 的结果
- Summarize
	- 可以对来自不同表的列进行自动匹配，比如可以 `Summarize(Sales, 'Product'[Category], 'Date'[Calendar Year])`
- PowerBI 显示
	- 显示结果是已有列的组合
	- 并不是因为 **自动匹配** 机制
	- 而是增加了一个 隐藏的 CountRows


