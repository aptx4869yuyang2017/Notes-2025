---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
  - "[[DAX-上下文转换]]"
created: 2025-01-28
tags:
  - domain/powerbi
---
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
