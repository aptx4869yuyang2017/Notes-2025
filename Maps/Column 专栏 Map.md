---
up: []
related: 
created: 2025-07-22
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


