---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[优化DAX-CH02 案例介绍优化方案]]"
created: 2025-08-26
tags:
  - domain/powerbi/performance
---

[Feishu - Log in](https://rk7nrn34nu.feishu.cn/docx/LxsfdJCu6oHUvYxQ2ofcroeVnBf#share-XZo9dvUERoHM54xo0bmcP3pDnig)


> [!important] 是否要空间换时间
> **关于是否使用计算列的简单决策，需要经过多方面的考量与测量**。更重要的是，**了解决策背后的依据本身就具有重要价值**


![image.png|729](https://s1.vika.cn/space/2025/08/26/42ae71983ca14f088893d018156d5257)

提前计算列确实能提升计算速度，但是会极大占用存储空间


![image.png|481](https://s1.vika.cn/space/2025/08/26/ebb2d62f4c5e44c097e83a58260b1b45)
这三个计算列共占用9.6GB内存，显著增加了模型体积。