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



![image.png](https://s1.vika.cn/space/2025/01/29/aaf83b1c9c4d4ff6a047e2f1986c2f68)


![image.png](https://s1.vika.cn/space/2025/01/29/af9df6b08a9e4ce9a68792b1195fbab3)

不要想太多：就是使用 Sales Amount / NumOfWorkingDays 解决这个汇总粒度数据不对的问题


# 基础版本

![image.png](https://s1.vika.cn/space/2025/01/29/8fc748e9f65c4ca3a37d27f833a0fa02)

![image.png](https://s1.vika.cn/space/2025/01/29/ac72c520aa9f4954b021503437b61b56)

**注意年汇总比所有月都低**


# 改进版本

其实书里还有一个中间版本，我觉得没必要，直接上最终版本

注意这里其实就是用 [[DAX-迭代函数]] `SUMX` 在**需要的粒度上进行了必要的计算**（只保留有 
Sales 的月份）

![image.png](https://s1.vika.cn/space/2025/01/29/7879e10ff99d4a8d83463794fcc5c7ca)

![image.png](https://s1.vika.cn/space/2025/01/29/6cecb40121b7403f8030434f5f707e35)
