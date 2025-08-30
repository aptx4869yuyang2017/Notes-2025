

# 经济金融学习


- [x] [[货币银行经济学-CH03 金钱&国家 - 以美国为例]]
- [x] [[货币银行经济学-CH04-金钱的宏观&微观视角]]
	- [x] 海曼 明斯基 阅读材料
- [x] [[货币银行经济学-CH05-央行：清算所 Clearinghouse]]
- [x] [[货币银行经济学-CH06 联邦基金：最终清算]]
- [x] [[货币银行经济学-CH07 回购 Repo 延期结算]]
	- [ ] 中国的 隔夜拆借利率 vs 回购利率
- [x] [[货币银行经济学-CH08 欧洲美元 平行结算]]
- [x] [[货币银行经济学-CH09 白芝浩所知道的世界]]
- [x] [[货币银行经济学-CH10 交易商和流动性证券市场]]
- [x] [[货币银行经济学-CH11 银行和流动性市场]]
- [x] [[货币银行经济学-CH12 最后贷款人]]
- [x] [[货币银行经济学-CH13 货币究竟是什么]]
- [x] [[货币银行经济学-CH14 国际货币体系变迁]]
- [x] [[货币银行经济学-CH15 金本位-银行 全球流动性]]
- [x] [[货币银行经济学-CH16 外汇]]
- [x] [[货币银行经济学-CH17 直接与间接金融]]
- [x] [[货币银行经济学-CH18 远期合约与期货]]
- [ ] [[货币银行经济学-CH19 利率互换]]



- [[行业分析&个股投资(course)]]







# 投资框架



- [ ] [个股估值](https://akshare.akfamily.xyz/data/stock/stock.html#id284)
![image.png|292](https://s1.vika.cn/space/2025/04/13/5d5cf2e9431e41a0bfad804fddbebc10)
- ak.stock_a_indicator_lg 这个接口返回信息总有抓不到的

- [ ] [公司股本变动-巨潮资讯](https://akshare.akfamily.xyz/data/stock/stock.html#id144)

[[Python 投资组合优化与绩效评价]]

- 统计基础 [[通俗统计学原理入门]]

# 指标计算




**宏观指标**

- [生产总值](https://akshare.akfamily.xyz/data/macro/macro.html#id47)
- [社融增量统计](https://akshare.akfamily.xyz/data/macro/macro.html#id27)

- [银行理财发行数量](https://akshare.akfamily.xyz/data/macro/macro.html#id47)
- [原保险保费收入](https://akshare.akfamily.xyz/data/macro/macro.html#id27)
-  货币供应量  macro_china_supply_of_money

[国债收益率曲线](https://akshare.akfamily.xyz/data/bond/bond.html#id15)



# 输出

- [x] [[Output-202504-PowerBI + Git + GitKraken：轻松可视化版本管理]]
- [x] [[Output-【哪吒2】票房预测的补充 1]]
- [x] [[Output-202505-PowerBI + Trea + Claude 自动化仪表板生成]]

[[Output-三种方式实现帕累托分析]]
- [[最大回撤的计算]]

- **IF 性能**
	- DAX
	- Tableau 如何控制条件，减少判断


【AI 自定义图表挑战 】
- Deneb 01 - 热力图 - 每日饮水量



【投资统计学】
- [正太分布-判断市盈率](https://www.bilibili.com/video/BV1j292YiEQu/?spm_id_from=333.788.top_right_bar_window_default_collection.content.click&vd_source=6d4ef5f8b8b73d69ea854cb9321a50ac)
- 线性回归-与市场的相关性
	- ![image.png|294](https://s1.vika.cn/space/2025/03/14/0e29fe94f78d4f90a9c2d5d76f5f1a53)
	- 美国的股票风险溢价：观察从1960年到最近一年美国股市隐含的股票风险溢价。


**定投到底能不能赚钱-可视化分析**
	- 定投赚钱的真相：从数据到策略的全方位测试


# BI


- [Data Goblins](https://data-goblins.com/articles)
- [BI Bites](https://nastengraph.substack.com/)

> [!NOTE]- PowerBI
> Todo



# 笔记统计

```dataview
TABLE length(rows) AS "月度笔记数量"
WHERE file.name
GROUP BY dateformat(file.cday, "yyyy-MM") AS 月份
SORT rows[0].file.cday DESC
```

