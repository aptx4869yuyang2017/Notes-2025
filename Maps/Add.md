---
up:
  - "[[00-Home]]"
related:
created: 2022-01-01
obsidianUIMode: preview
tags:
---


这个 **ADD** 笔记不仅仅是一个收件箱。它是一个冷却垫 🧊。
思绪汹涌而来。但几天后，它们就会冷却下来。
当冷静的想法占据上风时，你就能更好地确定优先顺序。Cool？


```base
filters:
  and:
    - file.folder == "+"
    - (today() - file.ctime) > "6 days"
formulas:
  Days: today() - created
  Live Days: today() - created
  Show: now() - file.ctime
views:
  - type: table
    name: Table
    order:
      - file.name
      - formula.Live Days
      - formula.Untitled
    sort:
      - property: file.ctime
        direction: DESC
    limit: 30
```