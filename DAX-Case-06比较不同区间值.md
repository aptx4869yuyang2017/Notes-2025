---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-设计模式(book)]]"
created: 2025-02-11
tags:
  - domain/powerbi
---

# 需求1 对比两个时间区间销售额

![image.png|426](https://s1.vika.cn/space/2025/02/11/e1594e6a8cb1408a83b0ccef48dd8fa5)

## 模型

![image.png|428](https://s1.vika.cn/space/2025/02/11/07e2f7e07afb423e8dba86ed4aebd112)

![image.png](https://s1.vika.cn/space/2025/02/11/1ff90251e3174526a10c30c6a45d6a85)


- 启用两个 Date 表之间的关系
- 移除原始 Date 表的筛选效果
- 保留 Comp Date 表的所有天数
- 筛选结果

# 需求2 对比修正后的时间区间销售额


![image.png](https://s1.vika.cn/space/2025/02/11/d7f18313f8e64f9591d9095b956c38b5)
![image.png](https://s1.vika.cn/space/2025/02/11/7bf5600aa9c642beb20c7852e1a3622f)

- 计算上下文 Date/Comp Date 天数
	- Values
	- countrows


Comp Sales x （Date 天数 / Comp Date 天数 ）