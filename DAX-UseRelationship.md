---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
created: 2025-01-29
tags:
  - domain/powerbi
---
# 基础用法：计算度量值

![image.png](https://s1.vika.cn/space/2025/01/29/61fc9d1a938d43bd9bdf9ca25c32109b)

![image.png](https://s1.vika.cn/space/2025/01/29/6acadfb6df314df281a032f412c3fe64)


# 延伸用法：计算特定条件下的度量值


> [!important]
> **关系**在**表引用被使用**的时候确定

## 方案一

![image.png](https://s1.vika.cn/space/2025/01/29/680327b03b0d425c8dcd19c6f7c207fb)

- Calculate 内部已经没有行上下文了，RELATED 会报错
- Sales 表引用被使用的时候，UseRelationship 没有生效

## 方案二


![image.png](https://s1.vika.cn/space/2025/01/29/15ebc540b9db4d2f8eee7c28cf28d4de)

- **依赖默认的筛选上下文传递比使用 Related 函数更好**

## 方案三

![image.png](https://s1.vika.cn/space/2025/01/29/d3c54f012950424cbc6ca659574f9e39)

- 标准做法
- UseRelationship 改变激活关系 ➡️  **筛选器参数的计值**





> [!important]
>  UseRelationship 需要**显示表引用**，所以在计算列中无法使用 UseRelationship

[[DAX-如何在计算列中使用非激活关系(TODO)]]