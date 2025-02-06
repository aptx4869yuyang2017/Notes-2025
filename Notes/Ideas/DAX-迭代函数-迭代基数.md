---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX-迭代函数]]"
  - "[[DAX 权威指南 - CH07 使用迭代函数Calculate组合]]"
created: 2025-01-11
tags:
  - domain/powerbi
---


[[PowerBI 性能 MOC|PowerBI Performance]] 
 
- Cardinality 基数，迭代表的行数
- 尤其注意 外层迭代的基数
	- 最内层的的迭代才能优化
	- 外部迭代器需要创建临时内存表，增加内存占用
- 嵌套迭代器，在大表上执行上下文转换会非常慢

## 迭代基数基础

![](https://s1.vika.cn/space/2025/01/11/eaed320502b247c4924cffb0cf00d8f9)

表有多少行，迭代基数就是多少

## 增加迭代关系

```
MEASURE Sales[Sales at List Price 1] =
	SUMX (
		Product,
		SUMX (
			RELATEDTABLE ( Sales ),
			Product[Unit Price] * Sales[Quantity]
		)
	)
```

- 因为内部外部表达式存在关系，外层迭代限制了每次迭代内部表达式都做了限制，所以本身迭代基数就是 Sales 行数


```
MEASURE Sales[Sales at List Price High Cardinality] =
	SUMX (
		VALUES ( 'Product' ),
		SUMX (
			Sales,
			IF (
				Sales[ProductKey] = 'Product'[ProductKey],
				'Product'[Unit Price] * Sales[Quantity],
				0
			)
		)
	)
```

- 因为没有不依赖关系，而是依靠 IF 判断，所以每次迭代一行 Product，都会完整迭代一次 Sales
- 所以迭代基数是 Product 行数 x Sales 行数

![](https://s1.vika.cn/space/2025/01/11/fc77c718f50c487d97a12e297bed1e4b)
- 查询计划中的表现是会存在一个 **CrossApply**（执行笛卡尔积）
- 如果 Filter 运算符在任何假 Spool 运算符之前执行，则 CrossApply 生成然后过滤的记录数不可见，您只能看到过滤的行数。**这里 Extend_Lookup 执行了 IF 操作过滤了数据**


```
MEASURE Sales[Sales at List Price 2] =
        SUMX (
            Sales,
            RELATED ( 'Product'[Unit Price] ) * Sales[Quantity]
        )
```



- 优化的写法
- 这个写法一个 SE查询就能搞定





```
MEASURE Sales[Sales at List Price 3] =
        SUMX (
            'Product',
            'Product'[Unit Price] * [Total Quantity]
        )
```


> [!note] 
> From a performance point of view, when there are nested iterators, **only the innermost iterator can be optimized with the more efficient query plan**. The presence of outer iterators requires the creation of temporary tables in memory. These temporary tables store the intermediate result produced by the innermost iterator. This results in slower performance and higher memory consumption. As a consequence, nested iterators should be avoided if the cardinality of the outer iterators is very large—in the order of several million rows.
> 
> 从性能的角度来看，当存在嵌套迭代器时，**只有最内层的迭代器可以使用更高效的查询计划进行优化**。外层迭代器的存在要求在内存中创建临时表。这些临时表存储由最内层迭代器产生的中间结果。这会导致性能变慢和更高的内存消耗。因此，如果外层迭代器的基数非常大——达到数百万行的量级——应该避免使用嵌套迭代器。







```
MEASURE Sales[Sales at List Price 5] =
	SUMX (
		'Sales',
		RELATED ( 'Product'[Unit Price] ) * [Total Quantity]
	)
```

- 最差的写法
- **大表/行不唯一 使用上下文转换** 


