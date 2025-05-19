---
up: []
related: 
created: 2025-05-13
tags:
---
![image.png](https://s1.vika.cn/space/2025/05/13/9d855957b1c94c1581866fef2b850d27)

```
#去掉ibooks引述
sed -E -e 's/^“//g' | sed -E -e 's/”$//g' | sed -E -e '/^$/d' | sed -E -e '/^Excerpt From$/,/^This material may be protected by copyright\.$/d'
```

![image.png|422](https://s1.vika.cn/space/2025/05/13/9189ea598f124d6881054b0e61ef9db6)

目前设定的是  `shift + cmd + c`

