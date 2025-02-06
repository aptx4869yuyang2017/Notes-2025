---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH07 使用迭代函数Calculate组合]]"
created: 2025-01-29
tags:
  - domain/powerbi
---

> [!important]
>   这个案例是 [[DAX 权威指南 - CH07 使用迭代函数Calculate组合]] 中为了讲解 迭代函数 + 上下文转换 的案例

> [!important]
>  使用迭代函数的一般思考方式
>  - **想要计算发生的粒度？**
>  - **希望计值的表达式？**
>  - **最后使用那种聚合？**

^c7559c


- 首先计算最大销售额，`MAXX` 肯定是必须用到的
- 但是计算销售额的方法有两种思路

# 需求1 计算一段时间内的最大日销售额



![400](https://s1.vika.cn/space/2024/03/26/cfd68d8ddb0f4f3a947051f0ef583ead)


着两个方案有什么 [[PowerBI 性能 MOC|PowerBI Performance]] 上的差异么？
## 方案一：使用 RelatedTable


![500](https://s1.vika.cn/space/2024/03/26/dceea1cc06214353b37f68507b1819ea)

- 迭代日期找最大
	- 计算当前行上下文的 Sales RelatedTable
	- 计算 Sales 的DailySales


## 方案二：使用上下文转换

![400](https://s1.vika.cn/space/2024/03/26/823ddb8acf6e4015b4f8c5f8e8ce2440)

利用上下文转换，计算度量值有了日期的筛选效果

## 总结

**两种计算指标筛选数据的方法**
- 行上下文
	- 一端表，RelatedTable 多端表实现筛选
- 筛选上下文
	- 筛选上下文筛选模型，所以不需要 声明 RelatedTable


# 需求2 计算最大日销售额所在日期


这里可以做一个 [[PowerBI 性能 MOC|PowerBI Performance]] 的案例
- 分析两次迭代的底层是如何执行的？
- 是：**查询计划中查询两个完全一致的结果**
 
## 基础版本

![400](https://s1.vika.cn/space/2024/03/26/65cf37edcfa44b1093b2c230cf431d0e)


![400](https://s1.vika.cn/space/2024/03/26/b606272242ba460ebff262623b224840)

## 优化版本


![400](https://s1.vika.cn/space/2024/03/26/e31525e37884499eaeb9c4c4d48d8d8d)
问题：迭代了两次 Date，每次都计算 Sales Amount
- 筛选上下文=1月，maxx 迭代 Date 找到最大 Sales Amount
- 再次迭代日期 找到等于 最大 Sales Amount 的日期 list


![360](https://s1.vika.cn/space/2024/03/26/be72ed7371914ac096b554fb2130658b)
![360](https://s1.vika.cn/space/2024/03/26/750126252d5c476d8f5ce460f9f2b239)

- 月筛选上下文下的：**日期 - Sales Amount 组合表**
-  迭代组合表，找 最大的日销售额
- 筛选组合表，保留有最大日销售额的 日期列

**两次迭代表都不再需要计算 每日销售额**

