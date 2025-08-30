---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[优化DAX-CH02 案例介绍优化方案]]"
created: 2025-08-26
tags:
  - domain/powerbi/performance
---
[Feishu - Log in](https://rk7nrn34nu.feishu.cn/docx/LxsfdJCu6oHUvYxQ2ofcroeVnBf#share-C9lmdSkifolyNBx90racg0D2nZc)

### 方案一：IF

![image.png](https://s1.vika.cn/space/2025/08/26/38b70e4480784c1d9fce12cb0f3af3da)


![image.png](https://s1.vika.cn/space/2025/08/26/959bb0bc97ac487192fdd084a5febcf0)

**有回掉，因为 SE 不支持 IF**

### 方案二：Calculate + Filter Sales 全表

![image.png](https://s1.vika.cn/space/2025/08/26/6ebc878dd86c4576a3636ea231d75012)

![image.png](https://s1.vika.cn/space/2025/08/26/51cce9026f954b11b6099d9e8d51bd22)
- 虽然我们删除了 CallbackDataID 并用 xmSQL 过滤器取而代之，但 VertiPaq 引擎还是检索了太多数据。
- 并不需要 检索 Quantity & Net Price
### 方案三 Calculate + Filter Quantity &Net Price 两列

**经验丰富的 DAX 开发人员都知道，CALCULATE 中的筛选器应在所需的最少列数上起作用，这样才能达到效果**

![image.png|542](https://s1.vika.cn/space/2025/08/26/5bbd4c8ffd524ed0ba48a0bbad56f324)


### 方案四 新版功能 - 直接写 Calculate 条件

