---
up:
  - "[[Unity-Godot Game Tools]]"
related:
  - "[[不使用教程的 Unity 学习法(youtube)]]"
created: 2024-04-21
---

- 我需要知道的事情(构建后续武器库的基石)
	- 脚本如何修改其他组件的信息
	- GameObject 如何与另外一个 GameObject 交流
	- 如何生成与删除GameObj
	- 当游戏物体之间发生碰撞，如何检测并作出反应
	- 如何制作 UI 音效 动画
	- 如何处理等级 gameover 之类的东西
	- ...

## Unity

### 如何脚本修改其他组件属性


- 定义类属性用于存放 组件
- `GetComponent<Rigidbody2D>()` 获取需要的组件
- 直接使用 点方法修改 组件属性


```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BirdScript : MonoBehaviour
{

    private Rigidbody2D myRigbody2D;

    void Start()
    {
        myRigbody2D = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) == true)
        {
            myRigbody2D.velocity = Vector2.up * 10;
        }
    }
}
```

![dfa618cfd82d4f1bae96b79b1f3d6fa3|279](https://s1.vika.cn/space/2024/04/21/dfa618cfd82d4f1bae96b79b1f3d6fa3)

代码提示可以看到 能够修改的属性 以及可用的方法

### GameObj 如何与另外一个 GameObj 交流

游戏对象不在场景时候引用一个组件

**通过 Tag 来找 GameObj**

`logic = GameObject.FindGameObjectWithTag("Logic").GetComponent<Logic>();`

![7cc418ddd7d54a1598712e4125d5accb|433](https://s1.vika.cn/space/2024/04/21/7cc418ddd7d54a1598712e4125d5accb)


### 如何生成与删除GameObj


`Instantiate(pipe, randomPosition, transform.rotation);`
`Destroy(gameObject);`


### 加载资源 Asset References

[Simple 2D Game in Unity: Snake | Asset References](https://youtu.be/Iz22-o7l6bc?list=PLzDRvYVwl53ucaUs0YGfyyKXdgqh5OtiK&t=515)

`snakeHeadSpriteRenderer.sprite = Resources.Load<Sprite>("Sprites/snakeHead");`

或者使用 GameAsset 管理资源

![](https://s1.vika.cn/space/2024/05/12/af6e810752014b2794fe50ad90c00686)

![](https://s1.vika.cn/space/2024/05/12/ece9a5abd82540208d420fa6dcae161b)


![[Pasted image 20240512175407.png]]




## Godot




### Scene 如何与另外一个 Scene 交流

#### 1 设定 % Unique Name

这种是预加载

`@onready var head: Head = %Head as Head`

使用 % 获取其他 Scene

#### 2 @export 类似 SerializeField-Public 可以在属性编辑器中绑定

这个也是预加载


#### 3 直接实例化 Scene

运行时加载到内存中
`var food_scene:PackedScene = preload("res://gameplay/food.tscn")`

```
var food = food_scene.instantiate()
get_parent().add_child(food)
```


#### 4 使用 Node - Group 获取

类似于 Unity 中 使用 Layer 找其他 GameObj

![8350f03d96c843bfa2b88f4dab15ca05|426](https://s1.vika.cn/space/2024/04/27/8350f03d96c843bfa2b88f4dab15ca05)


### 碰撞检测

使用 Area2D 中的信号

![](https://s1.vika.cn/space/2024/04/27/411c257e162248b3b30e3918c11992eb)



### 删除对象

```gdscript
func _on_area_entered(area):
	if area.is_in_group("food"):
		area.call_deferred("queue_free")
	else:
		pass
```

在物理周期结束时候释放，直接使用 queue_free 可能有问题


### UI

[Godot UI Basics - how to build beautiful interfaces that work everywhere (Beginners) - YouTube](https://www.youtube.com/watch?v=1_OFJLyqlXI)

- CanvasLayer 为了使 UI 层独立渲染
- Container 为了组织很多元素
	- GridContainer
		- how big do you want to be?
	- PannelContainer
		- 为了让背景能够自适应缩放，适应内部内容大小
	- MarginContainer
		- 设置边距
	- VBoxContainer
		- 内部元素垂直分布
- TextureRect 为了



![c8029c7d47f9404698a70d211280a071|285](https://s1.vika.cn/space/2024/04/29/c8029c7d47f9404698a70d211280a071)


- Contain 询问子节点需要多少空间
	- Expand 决定子节点能够使用多少空间
		- Stretch Ratio 决定分配比例
	- Shrink/Fill 决定自己诶单如何使用空间
		- 只 Fill 没有 Expand 并不会利用到所有空间
	- Spacer 一种剧中对齐的技巧


- 锚点
	- 将UI元素锚定到特定屏幕位置，并对窗口尺寸的变化做出反应
![58ced863012f4a3594848924838f1e16|278](https://s1.vika.cn/space/2024/04/30/58ced863012f4a3594848924838f1e16)

两个影响缩放效果的设定
长宽比/分辨率 改变 游戏界面/UI 如何变化

![bd76638905b94e708a09e1e99bfb615a|388](https://s1.vika.cn/space/2024/04/30/bd76638905b94e708a09e1e99bfb615a)


### 保存数据



### 瓦片图概念

![a72a9da3ced8489dad649d60456daa02|492](https://s1.vika.cn/space/2024/05/01/a72a9da3ced8489dad649d60456daa02)

- Tileset 是基础元素的集合
	- shift + 点选可以合并多个基础元素
- Tilemap 是基础元素的组合


### 动画设置

- AnimatableBody2D
- 增加 AnimationPlayer Node
- 


### 节点使用

- Area2D 不希望发生碰撞，但是可以检测到碰撞
- 玩家 CharacterBody2D