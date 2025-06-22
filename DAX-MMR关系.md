---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH15 高级关系]]"
created: 2025-06-10
tags:
  - domain/powerbi
---
# 1 桥接表实现

![image.png|596](https://s1.vika.cn/space/2025/06/10/68d84a0970624bfaac64d7af5d00740b)

## 问题

AccountsCustomers 筛选效果无法传递到 Transactions

![image.png](https://s1.vika.cn/space/2025/06/10/86883b17ebd74505a8c4a452fc9e702c)

尽管公式有很多变化，但所有这些解决方案都可以被归纳为两类:
• 使用 DAX 的 双向交叉筛 选器设置。
• 使用表作 CALCULATE 的筛 选器参数。

## A：双向交叉筛选

```jsx
SumOfAmt CF = 
CALCULATE ( 
    SUM ( Transactions[Amount] ),
    CROSSFILTER ( AccountsCustomers[AccountKey], Accounts[AccountKey], BOTH ) 
)
```

[[DAX-CrossFilter]]

## B ：使用表作为 Calculate 的筛选器参数

### 使用 Summarize 版本

```jsx
SumOfAmt SU = 
CALCULATE ( 
    SUM ( Transactions[Amount] ),
    SUMMARIZE(AccountsCustomers, Accounts[AccountKey])
)
```

注意

- `SUMMARIZE(AccountsCustomers, Accounts[AccountKey])` 仍然是在原始的计值上下文中计算
- `SUM ( Transactions[Amount] )` 部分才是在 Calculate 改变后的上下文中计算

这个参考 P125 中文版 CH05 理解 Calculate 部分

- 可以对 **来自不同表的列进行自动匹配** 详见 CH13 写查询 - Summarize 部分
- 所以保持了 Account 的 数据沿袭

### 使用 TreatAs - Values 版本

```jsx
SumOfAmt TA = 
CALCULATE ( 
    SUM ( Transactions[Amount] ),
    TREATAS(VALUES(AccountsCustomers[AccountKey]), Accounts[AccountKey])
)
```

- 先要思考为什么 单纯使用 Values 不行
    - 因为 桥接表 是多端，并不能反相筛选 Account
    - 但是 直接把结果当作是 Account 就可以继续筛选 Transactions 了

### 使用 拓展表 版本

```jsx
SumOfAmt ET = 
CALCULATE ( 
    SUM ( Transactions[Amount] ),
    AccountsCustomers
)
```

- 这里放了 AccountsCustomers ， 拓展表会延伸到所有的 1 端表
- 这张拓展表 会受到 Customer 列的筛选，同时其中的 Account 列可以作为 筛选 Transactions 的条件，实在是太妙了

## C： 不同方案之间的差异对比

差异主要
有的 Customer  Account 

![image.png](https://s1.vika.cn/space/2025/06/10/31c178f02c684ea49356c5f16c704cc6)
![Uploading file...rwwdg]()


使用关系进行交叉筛选，汇总部分不被筛选时候，就计算了总值

![](https://s1.vika.cn/space/2025/06/10/59057e8470704adaa87629488a33936d)

但是当使用表作为 Calculate 筛选参数时候，汇总值也不会计算没有匹配的关系

## D：最终建议

- 因为扫描 桥接表可能会有性能问题，所以只要能够保证数据一致性，那么推荐使用 双向交叉筛选
- 弱关系 也倾向于使用 双向交叉筛选

# 2 通过公共维度实现多对多关系

![image.png|685](https://s1.vika.cn/space/2025/06/10/880375c4b7244d4fb274f4efc70a88b1)


使用 TreatAs 移动筛选器
![image.png](https://s1.vika.cn/space/2025/06/10/6b45ffaa55a7470c86542a7d3ccfde30)
![image.png](https://s1.vika.cn/space/2025/06/10/e57259b28f4947e1b547b46cbf20c8f0)


- Budget 存在新产品，没有出现在 Product 中
- 没有使用效率最高的 物理关系

**添加新表同时作为 Budget / Customer 表的筛选器**

![image.png](https://s1.vika.cn/space/2025/06/10/ef53ce4a8e694a3f99ec699fa5a3320e)
![image.png](https://s1.vika.cn/space/2025/06/10/709df8027e8e4eaba266e4817f5a9209)

![image.png](https://s1.vika.cn/space/2025/06/10/3ac111353c5f4a229ad38ec74d040994)


进一步 调成称为双向交叉筛选，隐藏两个维度表

![image.png](https://s1.vika.cn/space/2025/06/10/e539070d3e86451a8036763827e748e1)

数据完备的情况

![image.png|605](https://s1.vika.cn/space/2025/06/10/3c16b7a6a5784802a5bcaf6b4fa3342f)

就算

![image.png|596](https://s1.vika.cn/space/2025/06/10/fc5d82d47bd5470f8124e113586e6180)


# 3 使用 MMR 弱关系实现多对多关系

**2018年10月新功能**

![image.png](https://s1.vika.cn/space/2025/06/10/6218a8a9d80c47ce8bba02c6e5dc44fa)


弱关系的问题是没有空行出现

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/06bdd6b2-e76d-4cfc-b000-2640a0d2ce9f/c6f7928b-40aa-4129-89b8-e19a8281a1a7/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/06bdd6b2-e76d-4cfc-b000-2640a0d2ce9f/d8d25be5-a42e-4614-a028-584609283b78/Untitled.png)

还是 更推荐使用公共维度来实现