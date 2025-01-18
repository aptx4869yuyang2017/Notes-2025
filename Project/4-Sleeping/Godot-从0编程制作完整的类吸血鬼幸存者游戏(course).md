---
up:
  - "[[Unity-Godot Game Tools]]"
related: 
created: 2024-04-10
tags:
  - domain/game
type: "[[Course]]"
finished: 
---
[从0编程制作完整的类吸血鬼幸存者游戏](https://www.bilibili.com/video/BV1s8411v7nE/?p=3&spm_id_from=pageDriver&vd_source=6d4ef5f8b8b73d69ea854cb9321a50ac)

- 01
	- 创建 Player
	- Player 移动
	- 创建 TileMap
	- Game Camera
- 02
	- 01 创建 Rat Enemy [[2024-04-13]]
	- 02 创建 剑技 [[2024-04-13]]
		- 信号
		- 运行时实例化scense
		- 输入变量
	- 03 AnimationPlayer 动画节点 [[2024-04-14]]
		- 动画编辑
		- 对象释放 queue_free()
	- 04 剑技目标设定 [[2024-04-14]]
		- list 使用 filter 过滤
		- distance_squared_to 直接返回的是距离的平方，因为开根比较消耗计算资源，所以可以直接对比平方
		- sort_customer 对 list 排序
		- list 使用 size 判断空值， 对象使用 == null
	- 05 摧毁敌人 [[2024-03-14]]
		- Area2D 节点的功能
			- 检测碰撞
		- 碰撞设定 Colission
			- Layer：我在这个层上，所以你可以和我碰撞
			- Mask：游戏里面的其他物体，我在这个层上，我想看看是否与你相撞了
	- 06 项目设定[[2024-04-15]]
		- 渲染抖动问题
			- project setting - render - 2D - Snap 2D Transform to Pixel - On
		- Debug 问题忽略
			- project setting - debug - GDScript - Ignore 对应的 Warnings
	- 07 自动生成敌人 [[2024-04-15]]
		- Godot 中的 场景起到了一部分 Unity 中 Prefab 的功能
			- 可以手工 实例化
			- 也可以动态实例化 instantiate
		- Manager 处理生成逻辑 / Enemy 处理移动逻辑
		- 以 player 为中心，四周生成 enemy
	- 08 提升游戏体验 [[2024-04-16]]
		- 移动有一点生硬
		- 摄像机有点延迟
		- enemy 有些会重叠
		- Motion Mode 修改为 Floatiing
	- 09 创建游戏循环基础 [[2024-04-16]]
		- 初步UI组件
			- MarginContainer - Label
		- 代码修改组件内容
	- 10 Experience Drops
		- 
	- 11 Tracking
	- 12 创建健康组建
