---
created: 2024-03-21
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "04"
finished: 2024-03-22
---

> [!NOTE]- TOC
> ![43a84a474163461bb5e141e96fb7ab4e|342](https://s1.vika.cn/space/2024/03/20/43a84a474163461bb5e141e96fb7ab4e)


本章与[[DAX 权威指南 - CH05 Calculate & CalculateTable]] 密不可分，两章常常需要反复阅读，理解记值上下文是学习 Calculate 的基础。
更完整的对计值上下文需要引入 [[DAX 权威指南 - CH14 DAX高级概念]] 中 [[DAX-拓展表]] 概念


本章对行上下文的介绍更多更详细，更多对筛选上下文的介绍要到后面章节。

- [[DAX-筛选上下文FC]]
	- 基础概念
	- 正式定义
	- 函数语意
- [[DAX-行上下文RC]]
	- 迭代表，计算列值
- 使用 **迭代函数** 创建 **行上下文** 
	- [[DAX-RC-迭代函数创建行上下文基础]]
	- [[DAX-RC-嵌套多个行上下文]] 
		- 多个表：多个行上下文同时生效
	- [[DAX-RC-多层嵌套行上下文]] 
		- 同一个表：外部隐藏，内部生效
			- [[DAX-Case-产品根据 Unit Price 增加排序计算字段]]
- [[DAX-理解Filter & All函数如何影响上下文]]
	- Filter 不改变筛选上下文，只是一个迭代函数
	- All 忽略筛选上下文，返回表的所有行
	- **这里也是 Tableau / PowerBI 思维方式差异的一部分，实际上 Tableau 完全是 Filter 思维，大部分逻辑都是得按照 Filter 的方式写，如果需要类似 All 的结果就得调整数据结构或者使用 LOD 了**
- [[DAX-计值上下文与关系]]
  *上下文是如何通过关系传递的*
	- 行上下文RC通过关系传递
		- 使用 Relate 多端获取1端信息 
		- 使用 RelateTable 1端获取多端的
		- 上下文关系链传递，在多v多环节
	- 筛选上下文FC通过关系传递 不需要函数
- 在筛选上下文中使用 Distinct 和 Sumarize
	- [[DAX-Case-Contoso 计算平均购买年龄]]
	- 理解 Distinct 和 Summarize 在这几计算平均购买年龄上的功能差异
	- 理解 在筛选上下文中 计算度量值是什么概念




