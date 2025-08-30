---
up:
  - "[[Power BI - Deneb]]"
related:
  - "[[Power BI - Deneb Medium 9 集课程]]"
created: 2025-07-22
tags: 
type: "[[Article]]"
finished: 
aliases:
---
![image.png](https://s1.vika.cn/space/2025/07/22/8be025940cfa4b08a7ede46fb5a6da41)


[Deneb & Vega-Lite Walkthrough Series \| EP03: STYLING MARK PROPERTIES (pt1)📊 \| by PBI DataVizzle \| Medium](https://pbi-datavizzle.medium.com/deneb-vega-lite-walk-through-series-ep03-styling-mark-properties-4dddb9e0f353)


# 基础结构

```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar"},        
  "encoding": {
    "y": {
      "field": "Category",
      "type": "nominal"
    },
    "x": {
      "field": "_AC",
      "type": "quantitative"
    }
  }
}
```


![image.png|502](https://s1.vika.cn/space/2025/07/22/557f5c6579dc4b9c88aae3c1d3bb15dc)



# 对轴排序


```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar"},
  "encoding": {
    "x": {
      "field": "Category",
      "type": "nominal",
      "sort": "-y"       // <-- sort the X-axis by the Y-axis (descending)
    },
    "y": {
      "field": "_AC",
      "type": "quantitative"
    }
  }
}
```

![image.png|525](https://s1.vika.cn/space/2025/07/22/d397bb54e65b4c82914afb4f2de409c3)

# Config 

[[Vega - Config]]

# 默认mark没有属性 vs 包裹mark标签可以编辑属性


```json
//** nb: comments and annotations added for effect **\\

{
  "data": {"name": "dataset"},
// observe the two varieties below
  "mark": "bar",            // <-- default mark, no properties {}
  "mark": {"type": "bar"},  /* <-- enclosing in curly brackets {} 
                            allows us to modify the different 
                            properties within the mark object
                            */

  "encoding": {
    "x": {...},
    "y": {...}
  }
}
```

# Fill  和 Color 的差异


[Mark \| Vega-Lite](https://vega.github.io/vega-lite/docs/mark.html#color)

![image.png](https://s1.vika.cn/space/2025/07/22/cab7f58b9f5f468a85af8a4f105abcdd)


# 柱形图调整列宽的4种方式



[[Vega - 柱形图调整宽度的四种方式]]


# 坐标轴的格式化

