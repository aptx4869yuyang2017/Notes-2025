---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH04 理解计值上下文EC]]"
created: 2024-12-08
---
#### 基础场景

![600](https://s1.vika.cn/space/2024/03/21/60d98527ac6b41f9822bd48cd887ed9b)

1. 在现有上下文中计值第一个参数以确定要扫描的行。  
2. 为在上一步中计值的每一行创建一个新的行上下文。  
3. 遍历表格并在现有计值上下文中计值第二个参数，现有计值上下文包括新创建的行上下文。 
4. 汇总在上一步中计算的值。  

我的理解：

1. 当前上下文 -> 确定要扫描的行
2. 在确定范围的表上 -> 计算第二个参数
3. 进行汇总第2步所有计算结果


#todo

> [!warning] 疑问
> 为什么非要说： 第二个参数的计算也受到外部上下文的影响呢？


文中给出的解答是：
 If the previous contexts already contained a row context for the same table, then the newly created row context hides the previous existing row context on the same table.
如果先前的上下文已经包含了同一表格的行上下文，那么新创建的行上下文将隐藏同一表格上之前存在的行上下文。

**难道不是个同一个表格，行上下文也没法共用啊！**

[[DAX-RC-嵌套多个行上下文]] 这里详细说明了怎么测试一下三个行上下文同时存在的情况

