---
up:
  - "[[Sources Map]]"
related: 
created: 2024-01-14
---
This note passively looks at the properties of all notes.

If a note has a `type` property that says `Book`, it will show up below.


> [!map]+ Article
> ```dataview
> table  created
> where type = [[Article]]
> sort created
> ```
