---
sourcePath: en/ydb/ydb-docs-core/en/core/reference/ydb-sdk/example/_includes/steps/01_init.md
---
## Creating a new driver, client, and session instance {#driver-client-session-init}

To interact with {{ ydb-short-name }}, you have to create an instance of the driver, client, and session:

* The {{ ydb-short-name }} driver lets the app and {{ ydb-short-name }} interact at the transport layer. The driver must exist throughout the {{ ydb-short-name }} access lifecycle and be initialized before creating a client or session.
* The {{ ydb-short-name }} client runs on top of the {{ ydb-short-name }} driver and enables the handling of entities and transactions.
* The {{ ydb-short-name }} session contains information about executed transactions and prepared queries, and is part of the {{ ydb-short-name }} client context.
