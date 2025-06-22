---
up:
  - "[[Econ Model 经济学模型 MOC]]"
related:
  - "[[货币银行经济学-CH10 交易商和流动性证券市场]]"
  - "[[资产定价模型 Asset Pricing Models]]"
created: 2025-06-02
tags:
  - domain/economy
dates: "1987"
---
# 模型基础教程

![image.png|314](https://s1.vika.cn/space/2025/06/02/b9acb267495a42f8afec8316126e183d)


![image.png|692](https://s1.vika.cn/space/2025/06/02/80b4faf72bfe45bcbb669cd8b1b9ff39)



- Y轴 Bond 价格
- X轴 Dealer 持有的 Bond 数量 (多头数量 or 空头数量)
	- 0 的左边 Short Position
	- 0 的右边 Long Position

三个关键元素
- **Outside Spread** :Long/Short 巴菲特愿意出的两种价格 
	- Value Based Bid 基于价值的出价
	- Value Based Ask 
- **[[融资流动性 Funding Liquidity]]**
	- 建立在资本/借贷容量基础上的 Position Limits / **Financing Limits**
- 两条斜线
	- 上斜线 卖出价格 Asked
	- 下斜线 买入价格 Bid
	- Bid Asked Spread 买卖价差


![image.png|366](https://s1.vika.cn/space/2025/06/02/76f75d1efff741afad12ca241a483061)

模型变化，假如银行能够给 Dealer 的支持变少
- 那么 Position Limit 收窄
- 相同库存下单报价 ⬇️


# Treynor做市商模型核心框架



**1. 库存与风险暴露**
- 做市商持仓方向决定风险敞口：
  • **多头库存**（正持仓）：价格上升盈利
  • **空头库存**（负持仓）：价格下跌盈利
- 极限头寸受制于：
  ✓ 资本金约束
  ✓ 银行融资额度（高杠杆特性）

**2. 双层价差结构**
- **外部价差（隐性）**：由"巴菲特型"基本面交易者锚定
  - **暴跌时提供价值买入底线**（流动性最后防线）
    - 比如市场下跌时候，我被迫大量买入债券，现金库存清空
    - 我只需要定一个比 Value-Based Bid 高一点的价格，吸收市场下跌债券，转手卖给巴菲特
    - 本质上是 巴菲特 给 Market Maker 提供了流动性
  - 狂飙时设定价值做空天花板
    - 本质上，上限也是由空头巴菲特的 Value-Based Ask 决定
  - 危机中外部价差消失→市场流动性枯竭
- **内部价差（显性）**：做市商实际报价
  - 买卖报价差（bid-ask spread）受两大因素驱动：
    (1) **波动率补偿**：高波动资产需更宽价差覆盖风险
    (2) **信息不对称防御**：防范知情交易者" Adverse Selection"

**3. 动态定价机制**
- 库存增加时自动调整报价（自我保护）：
  • 多头累积→降低买价（要求更深度折让）
  • 空头累积→提高卖价（要求更高溢价）
  - **订单流信息解读**：持续单边交易隐含未公开信息

**4. 流动性转换本质**


![image.png|460](https://s1.vika.cn/space/2025/06/02/801b0fe7bb84461aa1a87dae826a4f66)
![image.png|462](https://s1.vika.cn/space/2025/06/02/ebc72d962b19461b8b3b8efa1423fb2c)

- **[[融资流动性 Funding Liquidity]]**（银行融资）→ **[[市场流动性 Market Liquidity]]**（证券买卖便利性）
- 正常时期通过价差获利覆盖风险，危机时期传导链断裂

> 延伸阅读推荐：Larry Harris《交易与交易所》（市场微观结构实践指南）
> ****Trading and Exchanges***

[[交易与交易所 Trading and Exchanges(book)]]