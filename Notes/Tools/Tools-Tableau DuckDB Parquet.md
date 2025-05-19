[Tableau \| MotherDuck Docs](https://motherduck.com/docs/integrations/bi-tools/tableau/)

![image.png](https://s1.vika.cn/space/2025/04/03/5d058df2103b4d13b68de4fb3bc4caa5)


```
CREATE VIEW money_supply AS
	Select * 
	FROM read_parquet('/Users/yangyu/Data/InvestData/macro/money_supply.parquet');
CREATE VIEW gdp_monthly AS
	Select * 
	FROM read_parquet('/Users/yangyu/Data/InvestData/macro/gdp_monthly.parquet');
```


