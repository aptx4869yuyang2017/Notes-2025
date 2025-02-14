---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH16 DAX高级计算]]"
created: 2025-02-09
tags:
  - domain/powerbi
---
# 需求：构建计算列 订单序号 



![image.png](https://s1.vika.cn/space/2025/02/09/95d4a525ae444d08bf448f0eec6b8ded)

# 方案一：遍历两次 Sales

![image.png](https://s1.vika.cn/space/2025/02/09/620d9715b006418592035b3d4d41fa56)

# 方案二：构建 CustomerOrder 表

![image.png](https://s1.vika.cn/space/2025/02/09/5887e8cb7e7446ebba2272132663b9d8)


# 方案三：RankX 排序

```
Order Position = 
VAR CurrentCustomerKey = Sales[CustomerKey]
VAR CustomersOrders =
    ALL (
        Sales[CustomerKey],
        Sales[Order Number]
    )
VAR OrdersCurrentCustomer =
    FILTER (
        CustomersOrders,
        Sales[CustomerKey] = CurrentCustomerKey
    )
VAR Position =
    RANKX (
        OrdersCurrentCustomer,
        Sales[Order Number],
        Sales[Order Number],
        ASC,
        DENSE
    )
RETURN
    Position

```