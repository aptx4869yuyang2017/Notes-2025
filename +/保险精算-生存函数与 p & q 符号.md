---
up:
  - "[[Econ Fin Concept 经济金融概念]]"
related:
  - "[[短期与长期精算数学(course)]]"
created: 2025-08-29
tags:
  - domain/insure
---


The Survival Function, p and q Notation

[The Survival Function, p and q Notation - YouTube](https://www.youtube.com/watch?v=Qd_PMW702Qc&list=PLLXsDm32L84i6uq1jzGdkQclEcJdtfkS6&index=1)

![[生存函数]]


![image.png|465](https://s1.vika.cn/space/2025/08/10/edb3adb3bc7e4bb48cd93f4f641517c7)


累积分布函数 $F(t)$ ：超过2个月死亡；死亡的累积概率分布 $tq_x$
概率密度函数 $f(t)$ ：死亡事件的概率密度 $f_x(t)$ 
生存函数 $S(t)$:  超过 2个月还存活 $tp_x$

期望寿命 $\overset{\circ}{e}_{x}$ ：是对生存函数的积分

1.  **随机变量定义：**
    设 $T_x$ 为一个随机变量，表示一个当前年龄为 $x$ 岁的人的**未来寿命**。

2.  **符号表示法 ($p$ 和 $q$ 符号)：**
    *   **$_{t}q_{x}$**： 表示**累积分布函数 (CDF)**。
        *   定义： $_{t}q_{x} = P(T_x \leq t)$
        *   含义： 一个当前 $x$ 岁的人在未来 $t$ 年之内死亡的概率。
    *   **$_{t}p_{x}$**： 表示**生存函数**。
        *   定义： $_{t}p_{x} = P(T_x > t)$
        *   含义： 一个当前 $x$ 岁的人存活超过 $t$ 年的概率。
    *   **重要关系：** $_{t}p_{x} + _{t}q_{x} = 1$

3.  **概率密度函数 (PDF)：**
    $T_x$ 的概率密度函数 $f_x(t)$ 是其 CDF 的导数：
    $$
    \frac{d}{dt}(_{t}q_{x}) = f_x(t)
    $$

4.  **期望未来寿命：**
    一个 $x$ 岁的人的**期望未来寿命**记为 $\overset{\circ}{e}_{x}$。
    *   对于**连续型**随机变量，其计算公式为：
        $$
        \overset{\circ}{e}_{x} = E[T_x] = \int_{0}^{\infty} t \cdot f_x(t)  dt
        $$
    *   **关键推导结果（通过分部积分）：**
        可以证明上述期望值等价于：
 

![](https://s1.vika.cn/space/2025/08/29/f327155ad8804f4e8262423b5e2e8950)

   
这意味着**期望未来寿命等于生存函数曲线下的总面积**。
**积分上限说明：** 实践中，积分上限 $\infty$ 常被替换为最大年龄 $\omega$。