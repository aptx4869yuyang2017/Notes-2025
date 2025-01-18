---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH03 基础表函数]]"
created: 2024-11-30
tags:
  - domain/data
---
如何实现如下效果

![600](https://s1.vika.cn/space/2024/03/20/fa1d093dd7364179ad709ab65fb63be6)


- HasOneValue 
- SelectedValue


![600](https://s1.vika.cn/space/2024/03/20/a1c147d7f90941f2bcaed406afe6ae98)

**当 Values 值返回一行的时候，是可以被当作标量的**

![600](https://s1.vika.cn/space/2024/03/20/465cdcd898094a3aac7ef0db270631c1)

`Brand Name := SELECTEDVALUE ( 'Product'[Brand] )`
`Brand Name := SELECTEDVALUE ( 'Product'[Brand], "Multiple brands" )`


ConcatenateX

![600](https://s1.vika.cn/space/2024/03/20/c6bbfff3d0874af2bd123a2d0ac2659f)

计算(**表**)中每一行的(**表达式**)，然后在单个字符串结果中返回这些值的串联，并由指定的(**分隔符**)分隔。