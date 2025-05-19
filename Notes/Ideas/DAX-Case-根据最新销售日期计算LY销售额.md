---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH16 DAX高级计算]]"
created: 2025-02-09
tags:
  - domain/powerbi
---

# 需求：相同时间段同比


![image.png](https://s1.vika.cn/space/2025/02/09/775cd3c2d169481eb9d7708e0cf9a4e2)

![image.png](https://s1.vika.cn/space/2025/02/09/ff9e08755a214711a7a2989df9545cc0)

# 方案一：找到最新日期 构建可以同比的日期范围

![image.png](https://s1.vika.cn/space/2025/02/09/de6675d9f15347eea1d2457ea1187fba)

![image.png](https://s1.vika.cn/space/2025/02/09/578ba4b5437f4d228fcb54e5e7c1eaba)


# 错误方案：没有数据沿袭

![image.png](https://s1.vika.cn/space/2025/02/09/9f99c3daf2ad447d9fc1ebc6ead40dc5)

- 隐蔽 Bug
![image.png](https://s1.vika.cn/space/2025/02/09/48a6a0478ea8408dab5557e0db8d64e7)

SamePeriodLastYear 返回的是 Sales[Order Date] 上的去年日期，但是这个列有可能会缺失

下面是删除 2008-08-15 后的结果

![image.png](https://s1.vika.cn/space/2025/02/09/db88868ca2d84553a336030f44ea8062)


# 最优方案 构建计算列 - 能否参与同比


![image.png](https://s1.vika.cn/space/2025/02/09/42a11b41fb6e4e79be018e78bc0654a5)
