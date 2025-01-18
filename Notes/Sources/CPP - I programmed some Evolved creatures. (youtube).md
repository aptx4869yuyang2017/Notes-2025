---
aliases:
  - 编程可进化的生物
up:
  - "[[Simulation Map]]"
related:
  - "[[Project - 进化模拟项目]]"
  - "[[CPP Program Language]]"
tags:
  - domain/simulation
type: "[[Streaming]]"
created: 2024-01-21
finished: 2024-03-09
URLs:
  - https://www.youtube.com/watch?v=N3tRFayqVtk
---
[I programmed some creatures. They Evolved. - YouTube](https://www.youtube.com/watch?v=N3tRFayqVtk&t=1527s)
[davidrmiller (David R. Miller) · GitHub](https://github.com/davidrmiller)

---

## Index

![300](https://s1.vika.cn/space/2024/03/07/a14e8dd7cc3c406591840c087e88e852)

## The Conditions for evolution

> [!important] 进化与自然选择的5个条件
> - 自我复制
> - 每一个生物诞生必须根据某种蓝图构建
> - 蓝图继承 replicator -> replicant  |  parent -> offspring
> - 变异 Mutation
> - 选择 Selection




每一个生物体就是一个数据结构

![300](https://s1.vika.cn/space/2024/03/07/cadecea28c1f41bfb021026e640aa669)

- 位置
- 基因
- 神经网络：大脑


![300](https://s1.vika.cn/space/2024/03/07/cee217633d7349a3835f825d9b0e2aa6)

使用十六进制字幕代表基因


![300](https://s1.vika.cn/space/2024/03/07/02005f6cf86942d68f016002a3e2d41f)
变异方式

## Simulation #1 - How it works

![400](https://s1.vika.cn/space/2024/03/07/fe505c9d59c34c4ca0951c0d2a069d01)

![400](https://s1.vika.cn/space/2024/03/07/9e2f771b92c046cc98cf208d4c52daba)

- Step/gen 每代移动步数
- 每一个生物可以向八个方向移动，每代可以移动 300步数

![400](https://s1.vika.cn/space/2024/03/07/19743dafa5304e0f8827673d9a183732)

基因决定了 神经网络是如何连接的

![400](https://s1.vika.cn/space/2024/03/07/2f23dfd72b3b4bbd8f5f9e67d02ee0d6)
![400](https://s1.vika.cn/space/2024/03/07/3a63b111ef6442758f1895ad4c5e48c7)
![400](https://s1.vika.cn/space/2024/03/07/4eda62ed5af34426bd200baad4f09975)

![400](https://s1.vika.cn/space/2024/03/07/ed577901adb245ce9bd1bb3ffe46f540)

![400](https://s1.vika.cn/space/2024/03/07/3174e21540e841b7bd5c927edc9f0a08)

- 感知神经 感受前进方向的人口数量
- 两个移动神经，Mrn随机移动 MvE向东移动
- 内部神经选择要驱动的神经元

![400](https://s1.vika.cn/space/2024/03/07/3b977c418289493abeb9527e0ccea3ae)

随机抖动可以绕开障碍物


## 解刨大脑

![400](https://s1.vika.cn/space/2024/03/09/89ca087b9a544f96836a5cde71f67516)

![400](https://s1.vika.cn/space/2024/03/09/268acf66bcc94b449928116673a6c0d2)

一共有三大类的**神经元 Neuron**，而且是生物天生就有的
- 感知神经元
- 运动神经元
- 内部神经元

每一个基因定义了一个**神经连接**

![400](https://s1.vika.cn/space/2024/03/09/bcd1380542154286a2e9a5590e860b6f)

![400](https://s1.vika.cn/space/2024/03/09/75cc2b67b8d2446a89e6201fe947ba8e)

![400](https://s1.vika.cn/space/2024/03/09/ff67231f4a0f4352afd34b7cf3634c7c)

![400](https://s1.vika.cn/space/2024/03/09/c1c273431ce84acea6a987f39cfa3bc0)

- 链接的颜色和粗细代表了连接的权重
- 各种不同的连接方式
	- 感知 - 运动
	- 感知 - 内部
	- 内部 - 运动
	- 内部 - 内部

![500](https://s1.vika.cn/space/2024/03/09/398d95db62524f91a93ef1fd0a64118d)

- 所有的链接组合构成了大脑
- 从而决定了生物的行为方式

![400](https://s1.vika.cn/space/2024/03/09/0d33953d51014b7ebc0b89959740a53e)

没有的链接要排除计算

![400](https://s1.vika.cn/space/2024/03/09/ce486b7d2345430f94eda5372c597938)

- 输入 [0, 1]
- 链接权重 [-4, 4]
- 输出 `tanh(sum(inputs))` [-1,  1] 


![](https://s1.vika.cn/space/2024/03/09/ecb41b3526704c3b87bb738c8dbffa07)

感知输入

![](https://s1.vika.cn/space/2024/03/09/52db7ada1fda493f838891834beebe3a)


## Simulation # 2 变异与适应 Mutation and adaptation


![400](https://s1.vika.cn/space/2024/03/09/5dd1a1ede7d94048a509fd8f4319a92e)

![400](https://s1.vika.cn/space/2024/03/09/c000b13a7eb344e58ffa0836ed2c5532)

![400](https://s1.vika.cn/space/2024/03/09/a8f20cc098514a928a69f19f61fd7b79)

变异对重新适应环境有着重要作用

## 大脑规模

![300](https://s1.vika.cn/space/2024/03/09/8ae7bf14a66847dcb139d191445aca47)

![400](https://s1.vika.cn/space/2024/03/09/be61ecc3302a4ea8b73957bbb9f16c40)
![400](https://s1.vika.cn/space/2024/03/09/efa128ebb51f42e2b82b0b6d13648ad5)
![400](https://s1.vika.cn/space/2024/03/09/abc27607a4494615ba44030b623d7569)

![400](https://s1.vika.cn/space/2024/03/09/70e1e22d605444f4a9228eca779e6f8e)
![400](https://s1.vika.cn/space/2024/03/09/b170336a6ab84ff0947182ba97b789ba)

![400](https://s1.vika.cn/space/2024/03/09/3315cab0b11b4b8a8c7b1a430d1211ba)
![400](https://s1.vika.cn/space/2024/03/09/033c925bc89c4a9f86f14936fcf22764)

![400](https://s1.vika.cn/space/2024/03/09/1e53a3d42c51476e9a79cd6874f5dae4)

**神经是有价值的**

## 基因编码方式

8个十六进制数字
![200](https://s1.vika.cn/space/2024/03/09/ddf8037862dc48e49ff85de5db2330e3)
32个 2进制的数据

首先，将每个十六进制数字转换为四位二进制数：

- `f` 转换为二进制是 `1111`
- `1` 转换为二进制是 `0001`
- `3` 转换为二进制是 `0011`
- `5` 转换为二进制是 `0101`
- `1` 转换为二进制是 `0001`
- `f` 转换为二进制是 `1111`
- `e` 转换为二进制是 `1110`
- `3` 转换为二进制是 `0011`

![400](https://s1.vika.cn/space/2024/03/09/85630f5aa2434a4eb0842668f4a8fdf0)

## 杀手🥷基因

![400](https://s1.vika.cn/space/2024/03/09/caaf44ef88674c67920b7330314e68ed)

驱动信号足够强会杀死前进线路上的生物

![400](https://s1.vika.cn/space/2024/03/09/367f2069925c4175ab05b6f3e4179fed)
![800](https://s1.vika.cn/space/2024/03/09/897dc5e1c292412aaf8481208336336c)

![500](https://s1.vika.cn/space/2024/03/09/aa40fed4bd314daf9b3bf0ff075d040b)
![800](https://s1.vika.cn/space/2024/03/09/6885703292344959846550e5a917f008)

**经常有两个状态的切换，杀戮世代/和平世代**

有点像人类战争史

![600](https://s1.vika.cn/space/2024/03/09/4bb1ff7cf5334034b12399ed7cb5cde9)


## 代码简单介绍

![400](https://s1.vika.cn/space/2024/03/09/82de37537ba64134bc8daca8beaa3594)

![400](https://s1.vika.cn/space/2024/03/09/13ea310f74b2454a87e6c2c4d34529e7)

使用 CImg.h 来处理图像

![400](https://s1.vika.cn/space/2024/03/09/6d53af9ca17843dd96b15c706a9802f7)

![400](https://s1.vika.cn/space/2024/03/09/d6ddff748edc4eb29d098d146c537609)
画图使用了一个 python 库

![400](https://s1.vika.cn/space/2024/03/09/a769eab8465a4f059f2927385a831451)

日志记录

## Simulation #3 放射☢️区域挑战

放射源会改变位置



