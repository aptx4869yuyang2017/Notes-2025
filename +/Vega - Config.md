---
up:
  - "[[Power BI - Deneb]]"
related:
  - "[[Deneb Medium 9 集课程 - 03 修改 Mark 属性 pt1]]"
created: 2025-07-22
tags:
  - domain/powerbi
---
# Deneb 中的 Config 标签


![image.png](https://s1.vika.cn/space/2025/07/22/19587aad3b2743ddb12c4c39cc0499d2)


```json
{
  "view": {"stroke": "transparent"},
  "axis": {
    "title": false,
    "ticks": false,
    "grid": false,
    "domain": false,
    "labelColor": "#605E5C",
    "labelFontSize": 12,
    "titleFont": "din",
    "titleColor": "#252423",
    "titleFontSize": 16,
    "titleFontWeight": "normal"
  },
  "axisQuantitative": {
    "tickCount": 3,
    "grid": true,
    "gridColor": "#C8C6C4",
    "gridDash": [1, 5],
    "labelFlush": false
  }
}
```


![image.png](https://s1.vika.cn/space/2025/07/22/8e582bba1d574d78800cb718ffa49c92)

配置前后对比


# Config 配置说明


### Config.Mark 

[Mark \| Vega-Lite](https://vega.github.io/vega-lite/docs/mark.html#config)

这段文字是在解释 Vega 或 Vega-Lite 可视化语法中 `config` 对象的标记（mark）属性配置方式。我来用更简单的方式解释一下：

`config` 对象用于设置可视化的默认属性，特别是关于标记（marks，如条形、线条、点等）的默认样式。它有两种配置方式：

1. **全局标记默认设置** (`config.mark`)：
   - 这会应用于所有类型的标记（area, bar, line, point 等）
   - 示例：设置所有标记的默认颜色为红色
   ```json
   {
     "config": {
       "mark": {
         "color": "red"
       }
     }
   }
   ```

2. **特定标记类型的默认设置** (如 `config.area`, `config.bar`)：
   - 这只会应用于特定类型的标记
   - 示例：单独设置面积图(area)的默认颜色为蓝色，条形图(bar)为绿色
   ```json
   {
     "config": {
       "area": {
         "color": "blue"
       },
       "bar": {
         "color": "green"
       }
     }
   }
   ```

**优先级**：当两种设置冲突时，特定标记类型的设置会覆盖全局标记设置。比如如果同时设置了 `config.mark.color` 和 `config.bar.color`，那么条形图会使用后者指定的颜色。

这种设计让你可以既设置统一的默认样式，又能为特定图表类型定制特殊样式。

### Config.Style

[Mark \| Vega-Lite](https://vega.github.io/vega-lite/docs/mark.html#style-config)

这段内容讲的是 **Vega-Lite 中的命名样式（Named Styles）**，它允许你定义一组可复用的样式配置，然后在不同的标记（marks）或组件（如坐标轴、图例）中引用这些样式。这样可以避免重复定义相同的样式属性，使代码更简洁、更易维护。


#### **核心概念**

1. **`config.style`**  
   - 这是一个对象（`{ ... }`），用于定义**命名样式**（类似于 CSS 的 class）。
   - 每个命名样式可以包含一组**标记属性**（如 `shape`、`color`、`strokeWidth` 等）。
   - 之后可以在具体的 `mark` 定义中通过 `style: "样式名"` 来引用这些预定义的样式。

2. **如何使用命名样式？**
   - 在 `config.style` 中定义一个样式（如 `"triangle"`）。
   - 在 `mark` 定义中使用 `style: "triangle"` 来应用这个样式。

---

#### **示例解析**
##### 1. **定义命名样式**

![image.png](https://s1.vika.cn/space/2025/07/22/ac6c8ac695e642cc8c0b443ddb58d898)


```json
{
  "config": {
    "style": {
      "triangle": {          // 定义一个名为 "triangle" 的样式
        "shape": "triangle-up",  // 默认形状是三角形
        "strokeWidth": 2     // 默认描边宽度是 2
      }
    }
  }
}
```
- 这里定义了一个名为 `"triangle"` 的样式，它包含两个属性：
  - `shape: "triangle-up"`（形状是向上的三角形）
  - `strokeWidth: 2`（描边宽度为 2）

##### 2. **在 `mark` 中使用命名样式**

![image.png](https://s1.vika.cn/space/2025/07/22/3ae2269bedce43b799413d22445dcc89)

```json
{
  "mark": {
    "type": "point",      // 这是一个点图（散点图）
    "style": "triangle"   // 应用 "triangle" 样式
  }
}
```
- 这样，所有的 `point` 标记都会默认使用 `"triangle"` 样式（三角形形状 + 描边宽度 2）。

---

#### **内置样式（Built-in Styles）**

Vega-Lite 还提供了一些**内置样式名称**，用于控制坐标轴、图例、标题等组件的样式：

| 样式名 | 作用 |
|--------|------|
| `"guide-label"` | 控制坐标轴标签、图例标签、标题标签的样式 |
| `"guide-title"` | 控制坐标轴标题、图例标题的样式 |
| `"group-title"` | 控制图表主标题的样式 |

#### 示例：修改坐标轴标签的字体大小
```json
{
  "config": {
    "style": {
      "guide-label": {
        "fontSize": 14,    // 坐标轴、图例的标签字体大小设为 14
        "fontWeight": "bold"
      }
    }
  }
}
```
- 这样，所有坐标轴、图例的标签都会自动应用 `fontSize: 14` 和 `fontWeight: "bold"`。


### Config 案例

![image.png](https://s1.vika.cn/space/2025/07/22/7a0ded590ce943868238bd28807f6e5b)


```json
{
  "data": {
    "values": [
      {"a": "A", "b": 28},
      {"a": "B", "b": 55},
      {"a": "C", "b": 43}
    ]
  },
  "layer": [
  {
    "mark": "bar",
    "encoding": {
      "y": {"field": "a", "type": "nominal"},
      "x": {"field": "b", "type": "quantitative"}
    }
  }, 
  {
    "mark": {"type": "text", "style": "label"},
    "encoding": {
      "y": {"field": "a", "type": "nominal"},
      "x": {"field": "b", "type": "quantitative"},
      "text": {"field": "b", "type": "quantitative"}
    }
  }]
  
}
```


- 注意这里 text 的映射
	- x/y 说的是坐标映射
	- text 本身需要把数值映射出来

![image.png](https://s1.vika.cn/space/2025/07/22/2070cabf15e1424690632badd54a6869)


```json
{
"style": {
  "label": {
	"align": "left",
	"baseline": "middle",
	"dx": 5
    }
  }
}
```