---
sourcePath: en/ydb/ydb-docs-core/en/core/reference/ydb-sdk/example/_includes/steps/10_transaction_control.md
---
## Explicit TCL Begin and Commit calls {#tcl-usage}

In most cases, instead of explicitly using the [TCL](../../../../../concepts/transactions.md) Begin and Commit calls, it's better to use transaction control parameters in the execute calls. This helps you avoid unnecessary requests to {{ ydb-short-name }} and run your queries more efficiently.
