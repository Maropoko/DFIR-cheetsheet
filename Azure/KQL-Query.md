# KQL Query

## KQL Fundamentals
- take
  - take 10
- summarize
  - summarize count() by ColumnName
  - summarize NamedColumn = count() by ColumnName
  - summarize UniqueNameColumn = dcount(ColumnName)  # unique count
- top
  - top 10 by ColumnName  # equal to `summarize count() by ColumnName | sor by ColumnName desc | take 10`
- count
  - count
- project
  - project culumn1, column2, column3
- where
  - where ColumnName == "str"
  - where ColumnName contains "str"  # this is case-insensitive and finds partial matches, such as "str" and "strings".
  - where ColumnName has "str"  # this matches whole words, such as "str" only.  recommended.
  - where ColumnName startswith "str"  # suggested for searching IP address, email domains, or prefix.
- !=  # exclude singular
  - where ColumnName != "str"
- !in  # exclude multiplar
  - where ColumnNmae !in ("str1","str2")
- isnotempty
  - where isnotempty(ColumnName)
- ago
  - where timegenerated > ago(7d)
  - where timegenerated == ago(7h)
  - where timegenerated < ago(7m)
- and
  -  where condition1 and condition2  # equal to `where condition1 | where condition2`
-  extend
  - extend NewColumnName = sample
  - extend NewColumnName = iff(ColumnName == "str", "yes", "no")  # iff works like `iff(condition, value_if_true, value_if_false)`
  - extend NewColumnName = case(ColumnName == "str", "str", ColumnName == "int", "int", "other")
- parse_json
  - tablename
    | extend ParsedData = parse_json(JsonColumnName)
    | extend SpecifiedField = ParsedData.FieldName
    | summarize count() by tostring(SpecifiedField)  # KQL doesn't allow grouping by dynamic types
  - tablename
    | extend TargetData = parse_json(TargetResources)
    | extend TargetItem = tostring(TargetData[0].targetitem)

    
