```base
views:
  - type: table
    name: Table
    order:
      - file.name
      - file.ctime
      - file.mtime
    sort:
      - property: file.mtime
        direction: DESC

```
