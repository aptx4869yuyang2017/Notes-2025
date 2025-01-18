---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
created: 2025-01-01
tags:
  - domain/powerbi
---

Calculate 这个函数还是相当复杂的，目前这部分框架是 [[DAX 权威指南 - CH05 Calculate & CalculateTable||CH05-01]] 的内容

- **如果没有Calculate 应该怎么实现 vs Calculate 简化计算**
- **介绍 Calculate 操作上下文的原理**
- 调节器器介绍
	- **如何计算百分比（Calculate 与 [[DAX-All类函数||All类函数]] 的配合）**
		- All(dim[xx])
		- All(dim)
		- All(fact) - [[DAX 权威指南 - CH14 DAX高级概念]] 中 [[DAX-拓展表]] 概念
		- All(fact) + Values(dim[xx]) - 恢复某列的筛选效果
			- 可以用 [[DAX-All & AllExcept||AllExcept]] 替代这种方法
			- 但是语义不同 [[DAX 权威指南 - CH10 使用筛选上下文]] 会详细介绍差异
	- **[[DAX-KeepFilters]] 函数介绍**
		- 不覆盖
- 筛选参数拓展
	- **筛选单列**  `Sales[Net Price] >= 10 && Sales[Net Price] <= 100)`
	- **筛选复杂条件** `Sales[Quantity] ** Sales[Net Price] >= 1000)`
- **Calculate 计值顺序**
	- 由外向内层层覆盖


先整理了一个框架，后面懒得梳理了暂时 #todo

---



### 创建筛选上下文


- 基础语法
	- `CALCULATE ( Expression, Condition1, … ConditionN )`
- 相比使用 Filter 优雅简洁
- 但是和使用 Filter 的有功能上的差异


### 引入 Calculate



![600](https://s1.vika.cn/space/2024/03/23/e6fb83b7bc464a1ea848e3ab3280fa40)
![600](https://s1.vika.cn/space/2024/03/23/68552bb6545248448700844e4090c448)
![600](https://s1.vika.cn/space/2024/03/23/54bc7ef1bd21463dbe0147a49303ddf6)

- 完整语法格式，**值的列表**， 形式是一个 **表的表达式**
	- 结果可以是任意数量的列
- 布尔值 **语法糖**  #domain/powerbi/sugar
	- **语法糖不存在功能和性能上的任何差异** #domain/powerbi/performance 
	- 结果必须是**单值的值列表**
	





![500](https://s1.vika.cn/space/2024/03/23/c3046843cb69486eb51a6ecc4ec57dc8)


- 对筛选上下文的覆盖效果
- **只覆盖来自同一列的筛选器，合并不同列上的筛选器**

![](https://s1.vika.cn/space/2024/03/23/a80ac07849254c13acfca4775ec33200)

**语义**

- 复制筛选上下文
- 对 筛选参数 计值，给每一个列具体列生成一个 值的列表 list of values
- 如果两个条件对同一列生效，取**交集**
- 覆盖来自同一列的筛选上下文，不需要覆盖的就直接添加
- 用新的筛选，对 Calculate 的第一个参数进行 计值
- 恢复原始上下文


### 计算百分比

![500](https://s1.vika.cn/space/2024/03/23/20a0a866345e435fae19d07018aabcbd)
![500](https://s1.vika.cn/space/2024/03/23/1d63cfb6bd90491aa4a002ae3d21ef14)
![500](https://s1.vika.cn/space/2024/03/23/07e761351cc64d95b803379f509a3868)

- 这里的效果**不是 用了一个 值列表去替换 已经存在的筛选上下文**
- 而是直接移除了相关的筛选上下文
- 看起来是因为效率更高？

![600](https://s1.vika.cn/space/2024/03/23/507ea39dce2e4cedbd4be1d4199369e4)
![600](https://s1.vika.cn/space/2024/03/23/f63ae510661f4f48b71e4bbc831de8ba)
![600](https://s1.vika.cn/space/2024/03/23/2ae0f82a6c67439e8b03fbb9476b0533)
![600](https://s1.vika.cn/space/2024/03/23/9603c4bd09634fe0915f68e33894c578)

展示操作筛选上下文的不同技术

![600](https://s1.vika.cn/space/2024/03/23/604413a4bc244131ab9acf0d44b3429e)
![600](https://s1.vika.cn/space/2024/03/23/81fe1d17658b46599e1c72dc85bfbfba)

![600](https://s1.vika.cn/space/2024/03/23/d250a1735f7d4d0ba4fa7cf8683feec1)


`Values('Date'[Calendar Year])` **这句是在原始上下文中计值的**


### 由多个列构成的筛选条件

![500](https://s1.vika.cn/space/2024/03/23/2f4b22ff23c0452d8e7e73573dd8558b)

- 只能使用 值列表的方式，布尔值的语法糖不行
- 值列表是两个列值的组合

---

![600](https://s1.vika.cn/space/2024/03/23/5f2301e778d54778a9a12c8551b1d75e)

![600](https://s1.vika.cn/space/2024/03/23/7374b8dff4bb497b86de2ad07b0daf2f)

使用 KeepFilters 可以引入外部筛选器的影响

![400](https://s1.vika.cn/space/2024/03/23/2c856071cb4145918d58092249faeb36)

- 非最佳实践
- calculate 的非第一参数的参数计算，是使用外部的筛选上下文
	- 所以这个写法确实语义上和第一个一样
- 性能和结果准确性都有问题
	- [[DAX 权威指南 - CH14 DAX高级概念]] 中讨论细节


### 多层嵌套 calculate 计值顺序

![400](https://s1.vika.cn/space/2024/03/23/a3ea4a1dd5774fec849aa27ab838a641)

![400](https://s1.vika.cn/space/2024/03/23/2f03f3aaf6f94e06bd0b164d2e8f6470)

**内侧覆盖外侧，但是可以用 KeepFilter 保持外层的筛选**
