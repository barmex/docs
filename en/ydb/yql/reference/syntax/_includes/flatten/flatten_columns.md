---
sourcePath: en/ydb/ydb-docs-core/en/core/yql/reference/yql-docs-core-2/syntax/_includes/flatten/flatten_columns.md
sourcePath: en/ydb/yql/reference/yql-docs-core-2/syntax/_includes/flatten/flatten_columns.md
---
## FLATTEN COLUMNS {#flatten-columns}

Converts a table where all columns must be structures to a table with columns corresponding to each element of each structure from the source columns.

The names of the source column structures are not used and not returned in the result. Be sure that the structure element names aren't repeated in the source columns.

**Example**

```sql
SELECT x, y, z
FROM (
  SELECT
    AsStruct(
        1 AS x,
        "foo" AS y),
    AsStruct(
        false AS z)
) FLATTEN COLUMNS;
```