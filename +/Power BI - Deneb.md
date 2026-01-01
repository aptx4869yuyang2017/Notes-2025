---
up:
  - "[[PowerBI MOC]]"
related:
created: 2025-07-21
tags:
  - map
---

> [!map]+ 
> ```dataview
> table created
> where contains(up, this.file.link) and !contains(file.name, "Template")
> sort file.name
> ```

