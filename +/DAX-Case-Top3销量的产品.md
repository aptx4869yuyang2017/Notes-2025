---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-TOPN]]"
  - "[[DAX 权威指南 - CH13 写查询]]"
created: 2025-02-09
tags:
  - domain/powerbi
---

# 需求1: 普通 TOP


![image.png](https://s1.vika.cn/space/2025/02/09/f2a644a3798f4b31bd0251086da15528)



![image.png](https://s1.vika.cn/space/2025/02/09/e87d0fa3711a4f7f8f118e3a4db6c084)
![image.png](https://s1.vika.cn/space/2025/02/09/d9bea66409b448ec8a9adfedcfa3bf24)


# 需求2：展示具体 Sales Amount

![image.png](https://s1.vika.cn/space/2025/02/09/0ebbda9bab704cd6b22ae484095e7244)

- 使用 AddColumns 增加 Sales Amount 的列

![image.png](https://s1.vika.cn/space/2025/02/09/0d7b7606398d4c4eac2852322336cac7)


# 需求3: 当出现平局 增加排序规则保证 TopN 数量


![image.png](https://s1.vika.cn/space/2025/02/09/83081963bb2f423b9b190a446ea77fb6)


上述写法无法保证稳定的 Top4


![image.png](https://s1.vika.cn/space/2025/02/09/d80da47490204738b61dfdfc85205235)

可以增加一个排序规则保证没有平局


# 需求4: 展示没在TopN中的内容归到 Others 中

![image.png](https://s1.vika.cn/space/2025/02/09/103d879f6a5149d68d3e96beb6c77416)



![image.png](https://s1.vika.cn/space/2025/02/09/9f7708a7c520456dbc4c53f51e9af52d)
![image.png](https://s1.vika.cn/space/2025/02/09/fc699e58a60a40358f8fc03d12a6aa88)


- [[DAX-Row]]
	- 值转表
- [[DAX-Except]]
	- 存在左侧，右侧不存在
- [[DAX-Union]]
	- union 表

# 需求5: Others 排到最后


![image.png](https://s1.vika.cn/space/2025/02/09/9a5aa564640944bdbd269eae3c6f2081)

![image.png](https://s1.vika.cn/space/2025/02/09/7146097fe6e54135b5d4307545a2e34d)
