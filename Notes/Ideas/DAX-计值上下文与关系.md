---
up:
  - "[[PowerBI DAX 概念]]"
related:
  - "[[DAX 权威指南 - CH04 理解计值上下文EC]]"
created: 2024-12-08
---



![9892dde4a1d648018563f6b8b54f046f|638](https://s1.vika.cn/space/2024/03/21/9892dde4a1d648018563f6b8b54f046f)

- **注意 Product 和 Sales 是双向筛选**

**筛选上下文筛选整个模型，行上下文只迭代一个表**

## 行上下文在关系间传递

**行上下文传递需要使用 Related / RelatedTable 函数。**

#### 多端访问一端

`Sales[UnitPriceVariance] = Sales[Unit Price] – 'Product'[Unit Price]`

'Product'[Unit Price] 并没有可以生效的行上下文，所以需要使用 related ，

`Sales[UnitPriceVariance] = Sales[Unit Price] - RELATED ( 'Product'[Unit Price] )`


#### 一端访问多端

计算产品有多少销售订单行

![600](https://s1.vika.cn/space/2024/03/21/9d15ceddd3484e2f80e2bfc7a711cd6f)


#### 在关系链上传递

- Related & RelatedTable 的传递可以贯穿 [[DAX-关系链]]
- 但是要求 [[DAX-关系链]] 必须是 **同类型/同方向**
	- 1v1 关系不会造成关系链传递效果中断
	- 多v多 关系会传递效果会中断
		- Custom -> Sales
		- Product -> Sales 
		- Customer - Product 因为两个关系是反向关系，这个场景被称为 **多v多关系**
		- 一个客户会购买多个产品，一个产品也会被多个客户购买
	- #todo 这里有个需要双向测试一下效果

## 筛选上下文在关系间传递

**筛选上下文的传递受到 筛选方向的限制**

![600](https://s1.vika.cn/space/2024/03/22/0300c2fe5f844762ae1b68d76efb1807)
