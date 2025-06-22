
```
let
    源 = Odbc.DataSource("dsn=datalake_new", [HierarchicalNavigation=true]),
    IMPALA_Database = 源{[Name="IMPALA",Kind="Database"]}[Data],
    app_Schema = IMPALA_Database{[Name="app",Kind="Schema"]}[Data],
    mcp_prs_checklist_zp8_df_Table = app_Schema{[Name="mcp_prs_checklist_zp8_df",Kind="Table"]}[Data]
in
    mcp_prs_checklist_zp8_df_Table
```