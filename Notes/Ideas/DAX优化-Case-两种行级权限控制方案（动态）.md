---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[优化DAX-CH16 理解权限优化]]"
created: 2025-02-06
tags:
  - domain/powerbi
---

# 要求

## 权限表

![image.png](https://s1.vika.cn/space/2025/02/06/d92034dcaee84eafaf59bc1ef7159a46)
![image.png](https://s1.vika.cn/space/2025/02/06/f9305bbbb7b94f87b5de45275c8908d5)


# 方案一：DAX表达式 过滤 维度表/事实表


![image.png](https://s1.vika.cn/space/2025/02/06/ebb38d0777c3417183b174f56d37f092)

```
Customer[Continent] IN
    CALCULATETABLE (
        VALUES ( UserContinents[Continent] ),
        UserContinents[UserName] == USERNAME ( )
    )
```


**性能分析**


要观察过滤的目标表有没有超过 128k，不然容易变成回调

![image.png](https://s1.vika.cn/space/2025/02/06/27ee11cdbaa1404480514ae90d587a71)

![image.png](https://s1.vika.cn/space/2025/02/06/4f86ea33e455424987f081a557b34733)


# 方案二：过滤权限表 UserContinents 构建多v多关系

![image.png](https://s1.vika.cn/space/2025/02/06/c9fa5405c48e46a1a880d0db12cade22)


![image.png](https://s1.vika.cn/space/2025/02/06/1d8522b74a8f47a3958f43b79d0c8cbc)
