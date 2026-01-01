---
up:
  - "[[PowerBI Tricks]]"
related:
  - "[[SQLBI]]"
created: 2025-09-14
tags:
  - domain/powerbi
cover: https://s1.vika.cn/space/2025/09/14/58ddc369fd9a4d24bfef705c74369bba
---
![image.png|555](https://s1.vika.cn/space/2025/09/14/58ddc369fd9a4d24bfef705c74369bba)


---

Read the expression for the Workdays MTD measure and look at the image of the example query. The measure expression returns incorrect results where holidays and weekends return a wrong result <example>1/1/2016-1/4/2016 is 2303 but should be 1, 1/5/2016 should be 2, etc.</example>. Follow the logic described. Ask if you require clarification.

<logic>
* Workdays should cumulate from month start to month end
* Weekends and holidays should always have the same value as the previous workday
    * <example>1/9/2016 and 1/10/2016 should have the same value as 1/8/2016</example>
* If the month starts on a weekend or holiday, then the weekend or holiday should have the same value as the first workday that is not a holiday
    * <example>1/1/2016, 1/2/2016, 1/3/2016 should have the same value as 1/4/2016</example>
</logic>

Before you answer, search the web and check only the following references:
<references>
* DAX Guide: http://dax.guide/
* Microsoft Documentation: https://learn.microsoft.com/en-us/dax/
* SQLBI: https://www.sqlbi.com/articles/
</references>

---

---


请阅读“本月至今工作日”（Workdays MTD）度量值的表达式，并查看示例查询的图片。该度量值的表达式返回了错误的结果，其中节假日和周末显示了不正确的值<示例>2016年1月1日至2016年1月4日的结果为2303，但应为1；2016年1月5日应为2，依此类推。</示例>。请遵循以下描述的逻辑进行修正。如有需要，请提出澄清问题。

<逻辑>
* 工作日的计数应从每月的第一天开始累积，直至月底。
* 周末和节假日的值应始终与上一个工作日的值相同。
    * <示例>2016年1月9日和2016年1月10日的值应与2016年1月8日相同</示例>
* 如果某月的第一天是周末或节假日，则该周末或节假日的值应与该月第一个非节假日的工作日的值相同。
    * <示例>2016年1月1日、1月2日、1月3日的值应与1月4日相同</示例>
</逻辑>

在回答之前，请先搜索网络，并仅参考以下资料：
<参考资料>
* DAX指南：http://dax.guide/
* 微软官方文档：https://learn.microsoft.com/zh-cn/dax/
* SQLBI（中文文章）：https://www.sqlbi.com/articles/
</参考资料>