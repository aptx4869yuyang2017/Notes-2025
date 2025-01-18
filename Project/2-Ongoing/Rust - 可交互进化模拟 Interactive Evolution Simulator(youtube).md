---
up:
  - "[[Project - 进化模拟项目]]"
related:
  - "[[Rust Program Language Map]]"
tags:
  - domain/simulation
type: "[[Streaming]]"
created: 2024-03-03
finished: 
URLs:
  - https://www.youtube.com/watch?v=6nMo8T3T0L4&t=172s
aliases:
  - 交互进化模拟
---

## Blob 生存法则

- 每一代必须吃到一块食物并返回到边缘才能存活到下一代
- 如果得到了两块食物，就可以繁殖
- 寻找食物有固定的能量消耗
- 能量消耗取决于三个特征
	- **Sight Range 视野范围**
		- Blob 会以随机的方式进行移动
		- 有食物进入视野，向食物移动并吃掉食物
		- 除非有其他Blob 更快地吃掉食物
	- **Speed 速度**
		- 可以启用速度指示器，速度越快，颜色越红
	- Size 大小
		- 大的 Blob 可以吃小的 Blob，条件是尺寸大 20% 以上
		- 当然也必须有足够的速度追上小 Blob


> [!important] 和原版Primer的差异点
> 因为作者觉得Blob的尺寸应和速度有一定的关系
> 所以他把速度和尺寸结合了起来
> `get_speed(&self) -> f64 {self.speed * self.size / 10}`


![400](https://s1.vika.cn/space/2024/03/05/cade9cde42bd4726bbc9a3d05c8641c5)


![400](https://s1.vika.cn/space/2024/03/05/c4a5183e64784f41aa02ed7c4a1ae451)

- 更大的视野
- 更快的速度
- 对同类的捕食
**意味着更多的食物**

## 能量消耗公式

![600](https://s1.vika.cn/space/2024/03/05/0febf982ef754269bfb308cddd23c1a8)

![600](https://s1.vika.cn/space/2024/03/05/8f1fa9a77b284b81827761308947ba70)


查询一下 **动能公式 the formula for Kinetic Energy** 是个啥

## 繁殖过程设计

- 每次繁殖，特性数值会随机变大变小
- 新一代的 Blob 更容易继承优秀的父代特性
- 