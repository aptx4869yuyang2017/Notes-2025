---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX-Calculate]]"
created: 2025-01-05
tags:
  - domain/powerbi
---








```
CALCULATE (
	    Sales[Sales Amount],
	    'Product'[Category] = "Audio",
	    ALL ( 'Product'[Category] )
	)
```




> [!NOTE] 第一步 对显式筛选参数计值
> CALCULATE 会在原始计值上下文中求值所有显式筛选参数。这包括原始行上下文（如果有）和原始函数上下文。所有显式参数都在原始计算上下文中进行独立计算。一旦评估运算完成后，CALCULATE 就开始构建新的筛选上下文。

区分 
- **显式筛选参数** Explicit Filter Arguments
	- 这些是直接传递给 `CALCULATE` 的参数，它们是显式定义的筛选条件
- **隐式筛选参数** Implicit Filter Context
	- 当你在 Power BI 透视表中放置字段时，会自动创建隐式筛选上下文

![3c8f485dc10348a09796f85fbb303d03|496](https://s1.vika.cn/space/2025/01/05/3c8f485dc10348a09796f85fbb303d03)

**计值意味着找到值列表**


> [!NOTE] 第二步 复制原始上下文
> CALCULATE 复制原始计值上下文，以准备新的计值上下文。它会丢弃因为新的计算上下文不包含任何行上下文。


第二步解释
![eec05dcc122a4b9f82b397a864c5e146|447](https://s1.vika.cn/space/2025/01/05/eec05dcc122a4b9f82b397a864c5e146)


> [!NOTE] 第三步 CALCULATE 执行**上下文转换**
> CALCULATE 执行**上下文转换**。

![](https://s1.vika.cn/space/2025/01/05/552bc509ce4f49f890bfe8a4fecf3518)

- 这段描述的太绕了，简单解释
- 原始上下文 ➡️ 筛选行 ➡️ 每个单独列值都构成了一个筛选器 
- 不一定只筛选出一行数据
- **没有行上下文这一步会跳过**
- 所有行上下文转换形成的隐式上下文应用到了新的筛选上下文，进行下一步


> [!NOTE] 第四步 修改器计算
> UseRelationship CrossFilter All* 效果应用
> - **在第三步之后，意味着 All 可以移除 上下文转换的效果 [[DAX 权威指南 - CH10 使用筛选上下文||CH10]] 会详细介绍**

![](https://s1.vika.cn/space/2025/01/06/165ec1b4d1614bb6b0762e1788f2a556)

> [!NOTE] 第五步 计算隐式筛选参数
> - 算显式筛选参数的列值
> - 

![](https://s1.vika.cn/space/2025/01/06/481f57568eaf44ae8a75dcf85652dbbf)