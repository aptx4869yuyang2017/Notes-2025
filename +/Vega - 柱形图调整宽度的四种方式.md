---
up:
  - "[[Power BI - Deneb]]"
related:
  - "[[Deneb Medium 9 集课程 - 03 修改 Mark 属性 pt1]]"
created: 2025-07-22
tags:
  - domain/powerbi
---

# 1 Mark Width 固定值

```json
//** nb: comments and annotations added for effect **\\
{
  "data": {"name": "dataset"},
  "mark": {
    "type": "bar",      
    "color": "yellow",  
    "fill": "#F0E199",   
    "stroke": "#E044A7",
    "strokeWidth": 2,
    "width": 49          // <-- mark width 49px
  },
  "encoding": {
    "x": {...},
    "y": {...}
  }
}
```


# 2 Mark - Width 动态调整

```json
//** nb: comments and annotations added for effect **\\
{
  "data": {"name": "dataset"},
  "mark": {
    "type": "bar",      
    "color": "yellow",  
    "fill": "#F0E199",   
    "stroke": "#E044A7",
    "strokeWidth": 2,
    "width": {
      "expr": "bandwidth('x') * 0.85"    // <-- canvas bandwidth multiplied by 0.85
    }          
  },
  "encoding": {
    "x": {...},
    "y": {...}
  }
}
```