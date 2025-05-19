---
up: 
related: 
created: 2025-03-13
tags:
  - domain/stat
---


# t 值的概念


![image.png](https://s1.vika.cn/space/2025/03/15/10b0be4d49fe447aba9254cef5b9beff)



- **样本均值本身就是一个分布**
- t值：是每个抽样均值标准化的结果 
	- （ 【样本均值】 - 假设总体均值 ） /  [[统计-标准误差|标准误差]]

# t分布


![image.png](https://s1.vika.cn/space/2025/03/13/129303bac7e841a5bb8f096dca960147)


# t 检验




t检验是判断均值差异的常用工具，适用于小样本或总体标准差未知的情况，广泛应用于科学研究。

![image.png](https://s1.vika.cn/space/2025/03/13/f6b9ae8fc66748cb8f72e653afcc0799)






## 双边 t 检验

**双边检验**（Two-tailed test）用于检验统计量是否显著地不同于某个特定值，**关注的是差异本身，而不是方向**。它同时考虑统计量可能大于或小于假设值的情况。

- 适用于研究问题为“是否有差异”的情况
- 显著性水平α通常平分到分布的两侧
- 比单边检验更保守，需要更强的证据才能拒绝原假设


![image.png](https://s1.vika.cn/space/2025/03/15/dc2b33c0159546dbb5b1776880f126a3)


# 单边检验

**单边检验**（One-tailed test）是假设检验中的一种方法，用于检验统计量是否显著地大于或小于某个特定值，而不是简单地检验是否“不同”。




> [!NOTE] 单边检验 vs. 双边检验
> 单边检验：
> 只关注统计量在一个方向上的变化（大于或小于）。
> 例如：检验某投资策略的收益率是否显著高于市场基准。
> 双边检验：
> 关注统计量是否显著不同（无论大于还是小于）。
> 例如：检验某投资策略的收益率是否显著不同于市场基准。


```python
from scipy import stats

# 样本数据
data = [1, 2, 3, 4, 5]

# 假设的均值
pop_mean = 3

# 进行双尾 t 检验
t_statistic, p_value_two_tailed = stats.ttest_1samp(data, pop_mean)

# 单尾检验（左尾检验：检验均值是否显著小于 pop_mean）
p_value_one_tailed = p_value_two_tailed / 2  # 左尾检验
if t_statistic > 0:  # 如果 t 统计量为正，说明均值大于假设值，左尾检验不显著
    p_value_one_tailed = 1 - p_value_one_tailed

print(f"T-statistic: {t_statistic}, P-value (one-tailed): {p_value_one_tailed}")
```


[t 分布计算器网站](www.statdistributions.com/t/)

![image.png|454](https://s1.vika.cn/space/2025/03/15/08c7286a9feb49cb831987b9cc6ef3ca)

![image.png|454](https://s1.vika.cn/space/2025/03/15/1ba8bcb9e94f4afca331fc8987fbad22)

当 t 确定的时候，根据不同检验方式，p 追不同

