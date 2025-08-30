---
up:
  - "[[Econ Fin 经济金融 Map]]"
related: 
created: 2025-05-19
tags:
  - map
---

```base
filters:
  and:
    - up.contains(link("Econ Fin Event 经济金融事件"))
views:
  - type: table
    name: Table
    order:
      - file.name
      - dates
    sort:
      - property: file.name
        direction: DESC

```


