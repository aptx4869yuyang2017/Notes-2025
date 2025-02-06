---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[优化DAX-CH16 理解权限优化]]"
created: 2025-02-06
tags:
  - domain/powerbi
---



# 设定权限角色（两个不等于）

两个权限控制方式哪个会触发 **位图索引** 呢 [[DAX优化-位图索引]]

```
Customer[Continent] >= "Europe"

'Product'[Brand] >= "Contoso"
```

因为使用了 >= 所以可以被认为是 复杂筛选
Customer 表 >=


# 设定测试语句

`CustomerEurope,ProductContoso`

![image.png](https://s1.vika.cn/space/2025/02/06/67f5d3fc3f714fb2bd4afb50525833d4)
![image.png](https://s1.vika.cn/space/2025/02/06/5a0ac7ad0a324f0fb4bfd0ddb4e207fd)


# 查询语句分析

![image.png](https://s1.vika.cn/space/2025/02/06/48ea6c79542f46e4ab912409593b8526)

**注意这里 是使用 OR 条件，两个角色能看两个类型的数据，没问题！**


- CustomerEurope 使用了回调的方式限制
- ProductContoso 使用了 [[DAX优化-位图索引|位图索引]]


位图索引被 VertiCalc 条件使用




# 优化一：Customer表增加计算列规避回调


![image.png](https://s1.vika.cn/space/2025/02/06/5f69f317808c4959879ee80378746dee)

![image.png](https://s1.vika.cn/space/2025/02/06/f32449a4d4dd4793a3c7338982a76990)

因为将列转换为整数，所以不等于比较不需要调用 FE了

![image.png](https://s1.vika.cn/space/2025/02/06/002f8abd8968476e80a3056bdde8644e)

![image.png](https://s1.vika.cn/space/2025/02/06/8d73b41e4ae547cb8c73ed33368aa6aa)


# 优化二：Customer表中的 Contient 独立出一张隐藏表


![image.png](https://s1.vika.cn/space/2025/02/06/528c8ef4e6f24de88b9e21d8ccdf868b)
![image.png](https://s1.vika.cn/space/2025/02/06/fc0e6d8fd67b4bdf8276df247147ae43)
![image.png](https://s1.vika.cn/space/2025/02/06/b6e8afc21e1e4010a20d2f04cd6c014f)
![image.png](https://s1.vika.cn/space/2025/02/06/ffe775e1adab4d39a5b3acd5538ec307)
