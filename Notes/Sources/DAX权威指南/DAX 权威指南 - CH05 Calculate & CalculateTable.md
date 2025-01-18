---
created: 2024-03-23
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "05"
finished: 2024-03-23
---

> [!NOTE]- TOC
> ![400](https://s1.vika.cn/space/2024/03/23/054870541a054490a913441b99a3328b)
![400](https://s1.vika.cn/space/2024/03/23/e6b643db11784faab7fc45a5c61b2463)


# 介绍 Calculate / CalculateTable

- 本章以介绍 Calculate 为主
- CalculateTable 更多的示例
	- [[DAX 权威指南 - CH12 使用表函数 Work With Tables]] 
	- [[DAX 权威指南 - CH13 写查询]]

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




# 理解上下文转换

**Calculate 可以使行上下文无效，自动添加当前行上下文中迭代所有列作为筛选参数**


- 上下文转换开销很大
- 上下文转换不仅筛选一行
- 上下文转换会使用到公式中不存在的列
- 当行上下文被转换成筛选上下文的时候，就开始筛选整个模型了
- 只要有行上下文，使用 calculate 就会发生上下文转换
- 作用于所有行上下文
- 行上下文失效

### 1 计算列中的上下文转换

**没有key的表上执行上下文转换会非常危险⚠️**

### 2 度量值中的上下文转换

**每个被引用的度量值都被隐式封装在列 Calculate 中**


### 3 上下文转换造成的循环依赖问题

简单的循环依赖
![500](https://s1.vika.cn/space/2024/03/23/d10bbf0a6f60490ebc5d75b07485d15a)

**下面这组不容易识别到循环依赖问题**

`Sales[AllSalesQty] = CALCULATE ( SUM ( Sales[Quantity] ) )`
`Sales[NewAllSalesQty] = CALCULATE ( SUM ( Sales[Quantity] ) )`

第二个字段就会有循环依赖的问题
虽然看起来像是只依赖 `Sales[Quantity]` ，实际上因为上下文转换的原因 AllSalesQty 依赖的是 整个 Sales 表， `Sales[NewAllSalesQty]` 也是 Sales 表的一部分


![400](https://s1.vika.cn/space/2024/03/23/30e4f8ca72694443b6b77712ee3a4d5d)



`'Product'[ProductSales] = CALCULATE ( SUM ( Sales[Quantity] ) )`

- 在 Product 表上的上下文转换不会产生循环依赖问题。
- **只在唯一列上建立依赖关系**，仍旧使用所有列作为筛选参数的
	- 关系表位于一端
	- 某列被 Mark As Date Table (标记为日期表)， 有了隐式唯一列
		- [[DAX 权威指南 - CH08 时间智能计算]]



# Calculate 修改器

### UseRelationship

### CrossFilter

![600](https://s1.vika.cn/space/2024/03/23/132a2d74549c4f7386f4876997592d54)

### KeepFilters

![600](https://s1.vika.cn/space/2024/03/23/3c2de9e91eba497db1532d54661d38f2)

- 遍历 Color-Brand 组合表
- 因为在有行上下文的情况下使用度量值，有隐式Calculate，所以会发生上下文转换
- 所以 Color-Brand 会变成筛选上下文
- 使用 KeepFilters 可以保留外部筛选上下文的影响
- [[DAX 权威指南 - CH10 使用筛选上下文]] 会介绍一些例子


### All in Calculate

> [!error] 错误理解
> ![400](https://s1.vika.cn/space/2024/03/23/f8ab9d8f5b5f4cf090247bae5799f7ad)
> 

> [!important] 正确理解
> ![400](https://s1.vika.cn/space/2024/03/23/3055825904fc4b36bdad0c3832d24086)


- 本质上和 All 作为表函数是不同的功能
- 应该被称为 RemoveFilter 但是因为历史原因保留了这个名字
- Calculate 执行的筛选器参数也有执行顺序，All类会先执行

![400](https://s1.vika.cn/space/2024/03/23/fdebbc3070f344b68582ef05e25c422d)

这里感觉完全没说清楚，有需要的时候做测试吧

### 没有参数的 All / AllSelected

![300](https://s1.vika.cn/space/2024/03/23/c644936267204ae9ab3a0dc084ae3117)

清楚所有表中的筛选上下文，得到一个没有活动筛选器的筛选上下文

[[DAX 权威指南 - CH14 DAX高级概念]] 会深入介绍

# Calculate 计算规则