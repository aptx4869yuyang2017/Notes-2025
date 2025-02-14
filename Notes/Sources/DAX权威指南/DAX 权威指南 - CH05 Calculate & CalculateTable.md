---
up:
  - "[[DAX 权威指南(book)]]"
related:
  - "[[DAX 权威指南(book)]]"
created: 2024-03-23
tags:
  - domain/data
type: "[[Chapter]]"
ch: "05"
---

> [!NOTE]- TOC
> ![400](https://s1.vika.cn/space/2024/03/23/054870541a054490a913441b99a3328b)
![400](https://s1.vika.cn/space/2024/03/23/e6b643db11784faab7fc45a5c61b2463)

- [[DAX-Calculate]] 的介绍
	- [[DAX-Calculate-为什么需要Calculate]]
	- **如果没有Calculate 应该怎么实现 vs Calculate 可以通过创建筛选上下文简化计算**
	- 参数介绍：理解值列表
	- 基础语义：保留原始上下文 - 对筛选参数计值形成值列表 - 条件取交集 - **覆盖/添加筛选上下文** - 对第一参数计值 - 恢复原始上下文
	- 初步介绍两种调节器
		- 想要**移除已经**有的筛选上下文怎么办：[[DAX-Case-计算百分比]]
			- - All(dim[xx])
			- All(dim)
			- All(fact) - [[DAX 权威指南 - CH14 DAX高级概念]] 中 [[DAX-拓展表]] 概念
			- All(fact) + Values(dim[xx]) - 恢复某列的筛选效果
				- 可以用 [[DAX-All & AllExcept||AllExcept]] 替代这种方法
				- 但是语义不同 [[DAX 权威指南 - CH10 使用筛选上下文]] 会详细介绍差异
		- **不想覆盖**现有的筛选器怎么办：[[DAX-KeepFilters]]
	- 复杂筛选参数
		- **单表单列**  `Sales[Net Price] >= 10 && Sales[Net Price] <= 100)`
		- **单表多列** `Sales[Quantity] * Sales[Net Price] >= 1000)`
			- 多条件已经和书上描述的不太一样了：[[DAX-Calcualte-多条件筛选(21-03之后)]]
		- **多表多列** ：还是只能使用 CrossJoin 处理
	- **Calculate 计值顺序**
		- 由外向内层层覆盖
		- 使用 [[DAX-KeepFilters]] 之后有什么不同：取交集

- [[DAX-上下文转换]]
	- 计算列中的上下文转换 [[DAX-Case-高业绩产品]]
	- 度量值中的上下文转换
	- [[DAX-循环依赖问题]]

- 调节器
	- [[DAX-Calculate-筛选参数调节器]]
		- [[DAX-KeepFilters]]
	- Calculate 调节器
		- [[DAX-UseRelationship]]
		- [[DAX-CrossFilter]]
		- All 类函数
			- [[DAX-All & AllExcept]]
			- [[DAX-AllSelected]]
			- 作为调节器的使用 **可以没有参数**

- [[DAX-Calculate-计算规则]]
