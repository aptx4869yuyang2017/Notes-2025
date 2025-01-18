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


- [[DAX-筛选上下文]]
	- 基础概念
	- 正式定义
	- 函数语意
- [[DAX-行上下文]]
	- 迭代表，计算列值
- 使用迭代函数创建行上下文
	- [[DAX-Case-迭代函数创建行上下文基础]]
	- [[DAX-Case-嵌套多个表的行上下文]] 多个表：多个行上下文同时生效
	- [[DAX-Case-同一个表上多层嵌套行上下文]] 同一个表：外部隐藏，内部生效
- [[DAX-Case-理解Filter & All函数如何影响上下文]]
- [[DAX-计值上下文与关系]]
- [[DAX-在筛选上下文中使用 Distinct 和 Sumarize]]


----

