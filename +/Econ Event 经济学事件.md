---
up:
  - "[[Econ Fin 经济金融 Map]]"
related: 
created: 2025-05-19
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




> [!map]+ 备用
> ```
> table dates
> from #domain/economy 
> where dates != null
> sort dates
> ```

