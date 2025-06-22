---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-虚拟关系]]"
created: 2025-06-10
tags:
  - domain/powerbi
---


# 对比静态&动态分组

![image.png|363](https://s1.vika.cn/space/2025/06/10/4751be394b6c4ff5ba66891573bb0d7b)
- 静态分组是给 品牌价格区间分组
![image.png|345](https://s1.vika.cn/space/2025/06/10/0dc13ddcdb8c4203a3d4f2c57e65beb8)
- 动态分组是 对客户一段时间区间内的消费额度分组

# 目标 - 计算动态分组内的 客户数量


# 方案一 跨年份不累加

![image.png|469](https://s1.vika.cn/space/2025/06/10/dc05e452ec0e4c09b42b4240c46b64af)

![image.png|474](https://s1.vika.cn/space/2025/06/10/0b93a10261594901b99bf2c1fa3c61ef)

- 遍历 分组表 - 控制每个分组信息
- 客户数计算方式： CountRows 符合条件的客户
- 遍历 Customer 时候，计算 `[Sales Amount]`


