---
up:
  - "[[Sources Map]]"
related: []
created: 2022-01-01
---

> [!movie]+ Movie
> ```dataview
> table 
> 	dateformat(finished, "yy-MM-dd") as finished,
> 	short
> where type = [[Movie-Series]] and  !contains(file.name, "Template")
> sort created desc
> ```


