---
up:
  - "[[Sources Map]]"
related: 
created: 2024-01-01
---



> [!map]+ Book
> ```dataview
> table year, created, finished
> where type = [[Book📚]] and !contains(file.name, "Template")
> sort created desc
> ```
