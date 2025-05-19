---
up:
  - "[[Home]]"
related: 
created: 2025-05-14
tags:
  - map
---

> [!map]+ People
> ```dataview
> table dates, dateformat(created, "yy-MM-dd") as created
> where contains(tags, "people") and !contains(file.name, "Template")
> sort dates
> ```

```dataviewjs 
let pages = dv.pages("#books and -#books/finished").where(b => b.rating >= 7); for (let group of pages.groupBy(b => b.genre)) { dv.header(3, group.key); dv.list(group.rows.file.name); } ```
