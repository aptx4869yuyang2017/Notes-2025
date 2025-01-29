---
created: 2024-03-20
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "03"
finished: 2024-03-20
---

> [!NOTE]- TOC
> ![b11cf3dbd9754f0d975d16dcd7d7ed46|372](https://s1.vika.cn/space/2024/03/20/b11cf3dbd9754f0d975d16dcd7d7ed46)

本章重点是引入表函数概念，对表函数的详细介绍详见：[[DAX 权威指南 - CH12 使用表函数 Work With Tables]] [[DAX 权威指南 - CH13 写查询]]

- [[DAX-表函数]]
	- 函数参数，返回值同时都是表
	- 使用场景
		- 作为普通函数的参数
		- 可以用表函数定义变量
		- 嵌套其他表函数 -> **计值顺序**
			- RelatedTable [[DAX-RelatedTable]]
		- Calculated Table 计算表（虚拟表）
		- 使用 Evaluate 查询表
			- [[DAX 权威指南 - CH13 写查询]] 会深入介绍
		- 返回单一值的表函数可以被当作标量
			- [[DAX-HasOneValue & SelectedValue & ConcatenateX]]

- 常见基础表函数
	- [[DAX-Filter]]  迭代表，减少筛选数据
	- [[DAX-All & AllExcept]] 删除筛选状态
		- [[DAX-Case-Top类别子类别]]
	- [[DAX-Values & Distinct]]  获取唯一值表的两种函数
	- [[DAX-AllNoBlankRow]] All 函数的 Distinct 版本
	- [[DAX-AllSelected]] 能被切片器影响的 All


