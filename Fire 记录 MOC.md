---
up:
  - "[[00-Home]]"
related:
created: 2026-01-18
tags:
  - map
---
```base
filters:
  and:
    - up.contains(this.file.name)
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table
```

