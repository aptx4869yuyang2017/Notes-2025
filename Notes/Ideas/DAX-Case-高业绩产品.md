---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
  - "[[DAX-上下文转换]]"
created: 2025-01-28
tags:
  - domain/powerbi
---

这个案例是为了介绍 [[DAX-上下文转换]] 的一个案例，为了说明如何在计算列中使用上下文转换

> [!important] 需求
> 给 Product 表增加一个计算列，这个计算列用来给产品打一个 Flag ，如果这个产品的 销售额占整体销售额 1% 以上就是 High Performance product

![image.png](https://s1.vika.cn/space/2025/01/28/ae4e8a2f7017466e8dd54e379631cb96)


![image.png](https://s1.vika.cn/space/2025/01/28/1bb9d08220d74637b5dfe4d849f9b41e)
![image.png](https://s1.vika.cn/space/2025/01/28/79279aa9b33a4a3484e64e387c9e0957)


上下文转换的检查list
- Product 表是个小表，使用 上下文转换没有性能问题
- Product 每一行都是唯一的，不会有重复问题

## 错误案例

在 Sales 上使用 上下文转换
- 大表上下文转换性能不好
- 数据也不对，Sales 行不唯一

![image.png](https://s1.vika.cn/space/2025/01/28/0e678e4183c44026a04c0ce126427f06)
![image.png](https://s1.vika.cn/space/2025/01/28/cb119bad819046b88a23b256fac3463d)
