

```base
filters:
  and:
    - up.contains(this.file.name)
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table
    sort:
      - property: file.name
        direction: DESC

```