---
up:
  - "[[Home]]"
related: 
created: 2024-12-10
tags:
  - map
---

 
 
> [!map]+ Event
> ```dataview
> table 
> 	dates
> where contains(up, this.file.link) and !contains(file.name, "Template")
> sort dates
> ```


 
 
 
 
 ---
 
 *A concept is a pattern, truth, or mechanism that has been given a name.*
Just like the primordial goop that collided together billions of years ago to spark life on earth, so do these **conceptual** collisions spark exciting and diverse ideas. 

*概念是一种被赋予名称的模式、真相或机制。*
就像数十亿年前碰撞在一起引发地球生命的原始混沌物质一样，这些**概念性**碰撞也会引发令人兴奋和多样化的想法。

## Daily reminders of powerful concepts

Why not string out these ideas into paragraphs? What a way to unearth hidden connections!
为什么不把这些想法串成段落呢？这是发掘隐藏联系的好方法！

Starting some days, I'll consider how to apply three *strategic* mental models: [[OODA 循环]], [[Levels of Magnification 分析问题的三种级别]], and [[Refraction Thinking 折射思维]]. 



For more **avenues** to re-expanding my narrowed perspective, try to revisit the [[Rubik's Cube]], or pull from [[Munger's Mental Models 芒格的心智模型]].

为了寻找更多拓宽我狭窄视野的**途径**，尝试重新查阅  [[Rubik's Cube]] 或借鉴 [[Munger's Mental Models 芒格的心智模型]]。

---

Want to more deeply understand the flexible power of MOCs? Check out [[MOCs 鼓励灵活非破坏思维]] where you will see the same concepts above, in different ways.

---

# LYT Vision

Activate "LYT Vision" to resurface thoughts in context. When you twirl this open, it's like you are putting on night vision goggles: you see things hidden in the shadows.
激活 “LYT 视角”，让思想在语境中重现。当你打开它时，就像戴上了夜视镜：你能看到隐藏在阴影中的事物。

> [!Venetian]+ Unrequited notes
> These notes point directly to this note. But this note doesn't point back (yet). This is the strongest contextual query.
> 这些笔记直接指向这个笔记。但是这个笔记没有反向引用。这是最强的上下文查询。
> 
> ```dataview
> LIST
> 
> FROM [[概念 MOC]]
> and !outgoing([[概念 MOC]])
> and -#map
> 
> SORT file.mtime desc
> ```

> [!Venetian]- Unmentioned notes in common
> These notes share the tag `#concept` and are not mentioned above.
> 
> ```dataview
> LIST
> 
> FROM #concept
> and !outgoing([[概念 MOC]])
> 
> SORT file.name asc
> ```

---


Back to: [[Home]]