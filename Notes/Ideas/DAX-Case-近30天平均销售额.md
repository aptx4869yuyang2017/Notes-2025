---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH07 使用迭代函数Calculate组合]]"
created: 2025-01-29
tags:
  - domain/powerbi
---
# 需求


![|508](https://s1.vika.cn/space/2024/03/26/66227399071d4b2993bb4406d9430d33)

当指标波动剧烈的时候，可以使用近30天均值来做一个平滑方案

> [!important] 关键点
>  **没有 Sales 的天数是否参与均值计算？**


# 方案一 没有 Sales 的日期不参与均值计算


![400](https://s1.vika.cn/space/2024/03/26/067845572b1d488b8791365987ed91a4)

- 筛选上下文是 日期
- 如果区间的日期没有 Sales Amount 是不参与均值计算的


# 方案二 没有 Sales 也要参与均值计算



![400](https://s1.vika.cn/space/2024/03/26/1e06e6fc4ec242b9b644c1545778a0a1)

- 没有Sales 的日期也会参与均值计算

![image.png](https://s1.vika.cn/space/2025/01/29/28f43443d37246188555ddae57522f07)
