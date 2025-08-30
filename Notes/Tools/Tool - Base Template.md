


> [!NOTE]+ Data
> ```base
> filters:
>   and:
>     - up.contains(this.file.name)
>     - '!file.name.contains("Template")'
> views:
>   - type: table
>     name: Table
> ```


```base
filters:
  and:
    - up.contains(this.file.name)
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table
```