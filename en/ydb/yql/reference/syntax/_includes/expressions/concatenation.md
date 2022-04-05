---
sourcePath: en/ydb/ydb-docs-core/en/core/yql/reference/yql-docs-core-2/syntax/_includes/expressions/concatenation.md
sourcePath: en/ydb/yql/reference/yql-docs-core-2/syntax/_includes/expressions/concatenation.md
---
## String concatenation {#concatenation}

Executed using the binary operator `||`.

As with other binary operators, if the data on either side is `NULL`, the result is also `NULL`.

Don't confuse this operator with a logical "or": in SQL, it's denoted by the `OR` keyword. It's also not worth doing concatenation using `+`.

**Examples**

``` sql
SELECT "fo" || "o";
```
