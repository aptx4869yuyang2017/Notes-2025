---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH04 理解计值上下文EC]]"
created: 2024-12-08
---

#### 同一个表上多层嵌套行上下文

**需求：在 Product 表上根据 Unit Price 给产品排序**

![600](https://s1.vika.cn/space/2024/03/21/8260eddfe2624aa6abf33b2f9ee9a009)

- 会存在两个行上下文环境
- 使用变量能够让我们在需要的上下文环境中计值
- Earlier / Earliest 是 变量没有出现之前的，访问不同层级行上下文的一种方式

### Skip 模式

```
'Product'[UnitPriceRank] =
VAR PriceOfCurrentProduct = 'Product'[Unit Price]
VAR MoreExpensiveProducts =
	FILTER (
	'Product',
	'Product'[Unit Price] > PriceOfCurrentProduct
	)
RETURN
	COUNTROWS ( MoreExpensiveProducts ) + 1
```

![f79880f4ebff4ba18cf77ada0bee5795|433](https://s1.vika.cn/space/2024/12/08/f79880f4ebff4ba18cf77ada0bee5795)

![e2c618e9f99d4518a19883d241425280|441](https://s1.vika.cn/space/2024/12/08/e2c618e9f99d4518a19883d241425280)

### Dense 模式

```
'Product'[UnitPriceRankDense] =
VAR PriceOfCurrentProduct = 'Product'[Unit Price]
VAR HigherPrices =
	FILTER (
		VALUES ( 'Product'[Unit Price] ),
		'Product'[Unit Price] > PriceOfCurrentProduct
	)
RETURN
	COUNTROWS ( HigherPrices ) + 1
```

![ae67ff5d90704d2f85a8078e2b37e1f4|446](https://s1.vika.cn/space/2024/12/08/ae67ff5d90704d2f85a8078e2b37e1f4)