---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH04 理解计值上下文EC]]"
  - "[[DAX-Calculate]]"
created: 2025-01-28
tags:
  - domain/powerbi
---
# All 函数的移除筛选效果

> [!note] 
> **需求1: 计算特定展示维度下的百分比**


![500](https://s1.vika.cn/space/2024/03/23/20a0a866345e435fae19d07018aabcbd)

![500](https://s1.vika.cn/space/2024/03/23/1d63cfb6bd90491aa4a002ae3d21ef14)
![500](https://s1.vika.cn/space/2024/03/23/07e761351cc64d95b803379f509a3868)

- 这里的效果

> [!important]
> **不是 用一个 All 的值列表去替换 已经存在的筛选上下文**，而是直接**移除了相关的筛选上下文**

# 增加同一个表的维度


> [!note] 
> **需求2: 增加展示一个产品维度怎么办？**
> 1. 把新增加的列加入 All 中
> 2. 直接 All 整张 Product 表

![image.png](https://s1.vika.cn/space/2025/01/28/6a1c691cdee54b6d9d8f0ca0937f0684)


![600](https://s1.vika.cn/space/2024/03/23/507ea39dce2e4cedbd4be1d4199369e4)
![600](https://s1.vika.cn/space/2024/03/23/f63ae510661f4f48b71e4bbc831de8ba)

# 增加更多的表中的维度怎么办


> [!note] 
> **需求3: 增加展示更多其他的表维度怎么办？**
> 1. 继续把新的表添加到 All 中
> 2. 直接 All 事实表 Sales

![600](https://s1.vika.cn/space/2024/03/23/2ae0f82a6c67439e8b03fbb9476b0533)
![600](https://s1.vika.cn/space/2024/03/23/9603c4bd09634fe0915f68e33894c578)

# 如果不想移除某些筛选上下文怎么办？

> [!note] 
> **需求4: 计算当前年份总销售额的百分比
>  
> 1. 增加 Values 引入需要的筛选上下文效果
> 2. AllExcept

![image.png](https://s1.vika.cn/space/2025/01/28/74b69aeb6da0440e9049fc85f28e6389)


![600](https://s1.vika.cn/space/2024/03/23/604413a4bc244131ab9acf0d44b3429e)
![600](https://s1.vika.cn/space/2024/03/23/81fe1d17658b46599e1c72dc85bfbfba)

![600](https://s1.vika.cn/space/2024/03/23/d250a1735f7d4d0ba4fa7cf8683feec1)


`Values('Date'[Calendar Year])` **这句是在原始上下文中计值的**

## AllExcept 与 All + Values 的差异

[[DAX 权威指南 - CH10 使用筛选上下文]] 会详细解释两种写法的差异
- 这个案例明显不是 [[DAX-语法糖]]
- 两种写法会有差异