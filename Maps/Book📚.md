---
up:
  - "[[Sources Map]]"
related: 
created: 2024-01-01
---



> [!map]+ Book
> ```dataview
> table year,  dateformat(created, "yy-MM-dd") as created, dateformat(finished, "yy-MM-dd") as finished
> where type = [[Book📚]] and !contains(file.name, "Template")
> sort created desc
> ```

