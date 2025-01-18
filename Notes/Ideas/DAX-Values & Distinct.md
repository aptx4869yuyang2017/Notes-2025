---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH03 基础表函数]]"
created: 2024-11-30
tags: 
---

> [!important] 
> Values/Distinct 是可以被筛选影响的 All，返回**不重复的可见值**


![600](https://s1.vika.cn/space/2024/03/20/088ea7dbe473461aab4df6c9f4419227)


- 当关系无效的时候，会在 一端 的表上自动创建一个空行
	- 比如删除所有颜色为银色的产品
	- 尽管在 sales 表中有多个不同产品找不到 Producti 中对应的产品，但是实际上只有一个空行被添加
- **Values 将空行视作有效行，Distinct 函数并不返回空行**
	- 空被当作了value 但是不是distinct 的
	- *P71 FIGURE 3-12 这个案例没太理解，为什么第三列是对的，非空行也不一样呢* #TODO 
- Values Distinct **只能接受单列为参数**
	- [[DAX 权威指南 - CH12 使用表函数 Work With Tables]] 会提到 [[DAX-Summarize]] 来实现多列
- **两者常被用作 迭代函数 的参数**
- **Values 一般是默认选择， 除非有意排除空值**
- Distinct 代替 Values  可以解决循环引用问题 [[DAX 权威指南 - CH15 高级关系]]
- 可以接受表作为参数
	- Distinct 会剔除重复行，忽略空行
	- Values 不删除重复行，不忽略空行

> VALUES returns all the rows of the table, without removing duplicates, plus the additional  blankrow if present. Duplicated rows, in this case, are kept untouched.
> #TODO 这句话中的不移除 duplicates 是啥意思