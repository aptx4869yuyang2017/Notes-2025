---
created: ""
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "12"
---
# 使用 CalculateTable





#### 使用筛选条件，返回一个筛选表的两种不同写法

![](https://s1.vika.cn/space/2024/07/18/7d8d9ff3350445f98451b237cb3bb4bd)


#### 理解 CalculateTable 是如何修改上下文的


![](https://s1.vika.cn/space/2024/07/18/7d7e3f1f87e84552be33ad94a4c8b3a1)

> [!NOTE]
> changing the filter context first and later evaluating the expression

因为通过 CalculateTable 创建了一个筛选上下文，所以 CountRows 的计值是在 Color = Red 的条件下计算的
![](https://s1.vika.cn/space/2024/07/18/98e3ed3515b042d589d96519c5fe0634)

---

![](https://s1.vika.cn/space/2024/07/18/a7c6df4bc2bd48d4a18550983dd8d291)

在计算 Num of Products 时候，因为没有改变上下文，此时只有行上下文，CountRows 汇总需要筛选上下文，所以返回的是所有产品的行数

![](https://s1.vika.cn/space/2024/07/18/fcfd7ccb21514e61bf0a397e57a6b4b6)



![](https://s1.vika.cn/space/2024/07/18/66821d4ac73740f3adeb771f6e4d7f0d)

如果想要使用 Filter 得到正确的结果，那么必须改变使用函数的顺序
- 在遍历表的时候使用 Filter 函数
- 使用 Calculate 的上下文转换效果，应用 Filter 的结果

#### CalculateTable 不能使用的场景

**只能在 模型中有的列中使用筛选，不能使用度量值进行筛选**

![](https://s1.vika.cn/space/2024/07/18/4a56380dcbc64ca8bccabedc8e48271a)


#### 辅助参考

[CalculateTable 与 Filter 的差异](https://www.antaresanalytics.net/post/what-is-the-difference-between-filter-and-calculatetable)

> [!NOTE]
>  - **CALCUALTETABLE leverages the storage engine to modify the filter context**. 
>  - FILTER uses the formula engine to evaluate, row by row, a filter condition.
> 
> 不同引擎的使用


# Manipulating tables 操作表


# 使用表作为筛选器



# 创建计算表


