---
up:
  - "[[Sources Map]]"
related: 
created: 2024-12-04
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





