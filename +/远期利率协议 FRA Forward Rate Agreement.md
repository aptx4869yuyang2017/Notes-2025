---
up:
  - "[[Fin Tools 金融工具 MOC]]"
related:
  - "[[欧洲美元银行的流动性管理]]"
  - "[[货币银行经济学-CH08 欧洲美元 平行结算]]"
created: 2025-06-01
tags:
  - domain/economy
aliases:
  - 远期利率协议（FRA）的资产负债表视角分析
---


# 资产负债表分析法

最核心的工具是**远期利率协议（FRA）**，其本质是一种表外衍生工具，相当于对未来LIBOR利率的对赌。但用资产负债表内的视角更能理解其重要性。

假设：
- X银行预计2个月后要发放一笔3个月期美元贷款
- Y银行预计2个月后会收到一笔3个月期美元存款



### 传统操作（表内）


![image.png|528](https://s1.vika.cn/space/2025/06/01/752ab7a22a9d4584aad32b7ae8d5c185)

![image.png](https://s1.vika.cn/space/2025/06/01/846c85118f124bbdaa4b11320e1644b9)


1. 双方今日互换等值的资金承诺（IOUs）
2. 2个月后：Y银行向X银行支付存款资金
3. 5个月后：X银行向Y银行偿还贷款本息

### 效率优化1：初代方案（远期-远期合约）


  约定2个月后以固定利率F%存入3个月期存款，省略前2个月现金流


### 效率优化2：现代FRA

![image.png|643](https://s1.vika.cn/space/2025/06/01/56c229a37f9842c3b7072786b0001896)

  - 连本金交换也省去
  - 只需在2个月后结算LIBOR与F%的差额
  - 完全实现表外操作

### 核心功能

- X银行锁定最高借款成本（F%）
- Y银行确保最低投资收益（F%）
- 关键前提：双方确保能及时获得所需本金资金（该流动性假设在危机时可能失效）


# **远期利率平价**

**如何确定合适的远期利率F%？**

F%决定了未来贷款的资金成本和存款的收益，双方银行都需要合理定价：
- X银行希望F%越低越好
- Y银行希望F%越高越好

**关键定价原理：远期利率平价（FIP）**
假设市场存在：
- 2个月期LIBOR（当前至N=2个月）
- 5个月期LIBOR（当前至T=5个月）

通过构建以下组合可锁定2个月后的3个月远期利率：
**FIP公式**：
\[ [1+R(0,N)] \times [1+F(N,T)] = [1+R(0,T)] \]

![image.png](https://s1.vika.cn/space/2025/06/01/813fd263c2324330be9694d29c270c0d)

其中：
- R(0,N)：当前至N期的即期利率
- R(0,T)：当前至T期的即期利率
- F(N,T)：N期开始的T-N期隐含远期利率

**无套利本质**
若实际FRA利率偏离隐含远期利率：
1. 可在高利率端放贷
2. 在低利率端借款
3. 获得无风险利润

**市场实践**
实际远期利率必然趋近隐含远期利率——这正是银行间交易采用的定价基准。

