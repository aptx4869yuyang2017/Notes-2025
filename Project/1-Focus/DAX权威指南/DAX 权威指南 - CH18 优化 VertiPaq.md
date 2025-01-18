---
created: ""
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "18"
---

# 收集有关数据模型的信息
![](https://s1.vika.cn/space/2024/07/10/be32298d464545739a02a29097dcc3d4)

# 反规范化

[反规范化优化 - 一端表太大的问题 VertiPaq](https://www.notion.so/VertiPaq-2aeb250670f1494ca9ff023dfb725e3b?pvs=4)

# Cardinality

- 关系列键
	- 参考反规范化 [反规范化优化 - 一端表太大的问题 VertiPaq](https://www.notion.so/VertiPaq-2aeb250670f1494ca9ff023dfb725e3b?pvs=4)
	- 在度量值中聚合的数值
		- 数量/货币金额 不要改变京都
		- 如果是浮点型可以四舍五入到需要的小数位，减少 Cardinality
	- 低基数文本描述列：正常保留
	- 大基数大文本注释列：每行都是不同的，
	- 图片列：存url是更好的选择
	- 事务ID
		- 一般都有大基数，如果查询不需要，一定记得删除
		- 或者拆分成为 数值部分/字符部分 能够有效减少 Cardinality
	- 日期/时间：将该列分成 日期 / 时间 两列
	- 审计列：一般不要导入 VertiPaq


# 处理日期列与时间列

![](https://s1.vika.cn/space/2024/07/04/c477ddd823ab4d9d910a64405a21d952)

不同精度下的时间 Cardinality

尽量多选择 低精度的时间

# 计算列


可以使用计算列的场景

- 分组或者筛选数据
- 需要预计算的复杂公式

**不要错误地假设任何计算列都比具有相同租用的度量值更快**

**简单场景**

*方案一*

`Sales[Amount] = Sales[Quantity] * Sales[Price]`
`TotalAmountCC := SUM ( Sales[Amount] )`

*方案二*

`TotalAmountM := SUMX ( Sales, Sales[Quantity] * Sales[Price] )`

扫描单列的成本不一定比扫描两列的成本小。


**上下文转换场景**

```
AverageOrder :=
AVERAGEX (
	'Sales Header',
	CALCULATE (
		SUMX (
		'Sales Detail',
		'Sales Detail'[Quantity] * 'Sales Detail'[Unit Price]
		),
		ALLEXCEPT ( 'Sales Detail', 'Sales Header' )
	)
)

```


```
'Sales Header'[Amount] =
CALCULATE (
	SUMX (
	'Sales Detail',
	'Sales Detail'[Quantity] * 'Sales Detail'[Unit Price]
)

)
AverageOrder :=
AVERAGEX (
	'Sales Header',
	'Sales Header'[Amount]
)
```

存在上下文转换的场景，将值存储在计算列中可以节省计算时间

## 1 使用布尔类型的计算列优化复杂筛选器

![7d6dcd02b2f4479a96bbd5de4d3be0de|611](https://s1.vika.cn/space/2024/07/04/7d6dcd02b2f4479a96bbd5de4d3be0de)

![049fc261ed254e05a4a26194e379d968|616](https://s1.vika.cn/space/2024/07/04/049fc261ed254e05a4a26194e379d968)

生成只含有布尔类型的计算列
- 有非常好的压缩效果，使用了较少的内存
- 计算也比较高效，
## 2 为什么计算列会严重影响增量刷新的耗时？

- 刷新一张表的同时，需要对整个模型中重新计算引用了该表的计算列
- 比如增量刷新一张表，需要对引擎存储的所有计算列进行重新计算
- 计算列始终是在整表而不是单个分区中计算


#  存储合适的列

- 主键/备用健
	- 没有用到就不要放入 VertiPaq
- 定性属性列
	- 大基数大列要根据业务需求研判是否引入
- **定量属性列**
	- Price / Quantity / Amount 只计算平均价格如何取舍
	- 方案一：Quantity + Amount
		- Amount 的基数可能比较大
		- 数十亿行的大表，计算会更快
	- 方案二：Quantity + Price
		- 计算可能比较慢
		- 小表的时候删除 Amount 可能性能更好，对于个人电脑 内存占用越少打开越快
- **描述性内容**
	- 空值比较多，还能接受
	- 要是描述性的内容太多，可以使用复合数据模型，通过DQ访问描述性内容


# 优化列存储

## 1 列的拆分优化

常见拆分方法

字符串型
![](https://s1.vika.cn/space/2024/07/04/88cd102b49784ae9956f149e5844b786)

整型
![](https://s1.vika.cn/space/2024/07/04/26002dae0aa34df7abe0da2afff5731d)

十进制型
![](https://s1.vika.cn/space/2024/07/04/a9e5f518e5134bb4bbad9dddad6e886f)


- 以上优化的方向都是节省内存，如果是优化性能，不一定有用
- 比如数据类型如果是整型或者货币类型除非是使用值编码代替哈希编码

## 2 优化大基数列



## 3 金庸属性层级结构


## 4 优化钻取属性



# 管理 VertiPaq 聚合表


不能使用到聚合表的场景
![](https://s1.vika.cn/space/2024/07/04/c0d951d37c2342e88b8baa0deaf11dc5)