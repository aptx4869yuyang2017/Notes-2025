---
created: 2024-03-25
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "07"
finished: 2024-03-26
---

![600](https://s1.vika.cn/space/2024/03/25/bb2ac18a15654b3d9c54df35c20528f0)



## 使用迭代器

### 理解迭代基数

- Cardinality 基数，迭代表的行数
- 尤其注意 外层迭代的基数
	- 内部的迭代才能优化
	- 外部迭代器需要创建临时内存表，增加内存占用
- 重申：嵌套迭代器，在大表上执行上下文转换会非常慢

### 利用好上下文转换的功能

#### 任务一：最大日销售额的优雅写法（上下文转换版本）

![400](https://s1.vika.cn/space/2024/03/26/cfd68d8ddb0f4f3a947051f0ef583ead)



![500](https://s1.vika.cn/space/2024/03/26/dceea1cc06214353b37f68507b1819ea)

- 迭代日期找最大
	- 计算当前行上下文的 Sales RelatedTable
	- 计算 Sales 的DailySales

![400](https://s1.vika.cn/space/2024/03/26/823ddb8acf6e4015b4f8c5f8e8ce2440)

利用上下文转换，计算度量值有了日期的筛选效果

**两种计算指标筛选数据的方法**
- 行上下文
	- 一端表，RelatedTable 多端表实现筛选
- 筛选上下文
	- 筛选上下文筛选模型，所以不需要 声明 RelatedTable

#### 任务二：找到最大销售额所在的日期

![400](https://s1.vika.cn/space/2024/03/26/65cf37edcfa44b1093b2c230cf431d0e)

![400](https://s1.vika.cn/space/2024/03/26/b606272242ba460ebff262623b224840)

虽然像是废话，但是当想不清楚问题的时候，在重新按照 迭代函数的一般顺序思考一下

- **想要计算发生的粒度？**
- **希望计值的表达式？**
- **最后使用那种聚合？**




### 使用 Concatenatex

![400](https://s1.vika.cn/space/2024/03/26/dcfef6ec5151461383ab06235a1b46bc)

![500](https://s1.vika.cn/space/2024/03/26/2e723fa4a6a14f08934418e76f8d0d5f)


### 迭代返回表（AddColumns / SelectColumns）

即是表函数，也是迭代器

![400](https://s1.vika.cn/space/2024/03/26/bcdd9881f15946129e25a2b6828d3133)


#### 任务三：优化最大销售额所在日期写法
![400](https://s1.vika.cn/space/2024/03/26/65cf37edcfa44b1093b2c230cf431d0e)
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


## 使用迭代器解决常见问题


### 均值与移动均值 AverageX

![400](https://s1.vika.cn/space/2024/03/26/067845572b1d488b8791365987ed91a4)

- 筛选上下文是 日期
- 如果区间的日期没有 Sales Amount 是不参与均值计算的

![400](https://s1.vika.cn/space/2024/03/26/66227399071d4b2993bb4406d9430d33)


![400](https://s1.vika.cn/space/2024/03/26/1e06e6fc4ec242b9b644c1545778a0a1)

- 没有Sales 的日期也会参与均值计算


### RankX

#### RankX 语义顺序

![400](https://s1.vika.cn/space/2024/03/26/478e3b38d9074769a4cc7e9e98715027)

RankX 的执行步骤

- 构建查询表
	- 迭代第一参数
	- 在行上下文，使用第二参数计值
- 在筛选上下文对第二参数计值
- 返回 第二步计算结果在查询表中的位置

![500](https://s1.vika.cn/space/2024/03/26/4412d2ce7f834789a6f7e2b22ec32b38)

#### 避免 Total 返回排序

![400](https://s1.vika.cn/space/2024/03/26/386a1ab9da684789bfa5462e3c8cf23a)

![400](https://s1.vika.cn/space/2024/03/26/636c394f7d624d879fc6166869835e22)

**使用 HasOneValue 可以避免，在 Total 返回排序值**

#### 查询表与排序值使用不同的表达式

- 第三参数：表达式
- 第四参数：Asc/Desc
- 第五参数：Dense/Skip

![400](https://s1.vika.cn/space/2024/03/26/95c6855507564ed5b58569fa89883b44)

![500](https://s1.vika.cn/space/2024/03/26/8fded5e3492f4256a53405976992963d)
![600](https://s1.vika.cn/space/2024/03/26/20db95c7b4a04840829215dc40462df4)

### 修改计算粒度
