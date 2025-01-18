---
up:
  - "[[Sources Map]]"
related: 
created: 2024-01-01
---
This note passively looks at the properties of all notes.

If a note has a `type` property that says `Book`, it will show up below.


> [!map]+ Book
> ```dataview
> table year, created, finished
> where type = [[Book📚]] 
> sort created desc
> ```
