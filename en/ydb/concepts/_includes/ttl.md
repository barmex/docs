---
sourcePath: en/ydb/ydb-docs-core/en/core/concepts/_includes/ttl.md
---
# Time to Live (TTL)

This section describes how the TTL mechanism works and what its limits are. It also gives examples of commands and code snippets that can be used to enable, configure, and disable TTL.

## How it works {#how-it-works}

{{ ydb-short-name }} lets you specify a table column (TTL column), whose values set the lifetime of items. TTL automatically deletes the item from your table once the specified number of seconds passes after the time set in the TTL column.

{% note warning %}

An item with the `NULL` value in the TTL column is never deleted.

{% endnote %}

The timestamp for deleting a table item is determined by the formula:

```
expiration_time = valueof(ttl_column) + expire_after_seconds
```

{% note info %}

TTL doesn't guarantee that the item will be deleted exactly at `expiration_time`, it might happen later. If it's important to exclude logically obsolete but not yet physically deleted items from the selection, use request-level filtering.

{% endnote %}

Data is deleted by the *Background Removal Operation* (*BRO*), consisting of two stages:

1. Checking the values in the TTL column.
2. Deleting expired data.

*The BRO* has the following properties:

* The concurrency unit is a [table partition](../datamodel.md#partitioning).
* For tables with [secondary indexes](../secondary_indexes.md), the delete stage is a [distributed transaction](../transactions.md#distributed-tx).

## Guarantees {#guarantees}

* At every point in time, a *BRO* is run in no more than 1 instance per table.
* *BROs* are run no more than once per hour for the same shard.
* Data consistency is guaranteed. The TTL column value is re-checked during the delete stage. This means that if the TTL column value is updated between stages 1 and 2 (for example, with `UPDATE`) and ceases to meet the delete criteria, the row will not be deleted.

## Limitations {#restrictions}

* The TTL column must be of one of the following types:
  - `Date`
  - `Datetime`
  - `Timestamp`
  - `Uint32`
  - `Uint64`
  - `DyNumber`
* The value of the TTL column of the numeric type (`Uint32`, `Uint64`, or `DyNumber`) is interpreted as a value from the [Unix era](https://en.wikipedia.org/wiki/Unix_time) set in:
  - Seconds
  - Milliseconds
  - Microseconds
  - Nanoseconds
* You can't specify multiple TTL columns.
* You can't delete the TTL column. However, if this is required, you should first [disable TTL](#disable) for the table.

## Setup {#setting}

Currently, you can manage TTL settings using:

* [YQL](../../yql/reference/index.md)
* [Console client {{ ydb-short-name }}](../../quickstart/yql-api/ydb-cli.md).
* {{ ydb-short-name }}   Python [SDK](../../reference/ydb-sdk/index.md)

{% note info %}

TTL setup using YQL is possible for the `Date`, `Datetime`, and `Timestamp` columns.

{% endnote %}

### Enabling TTL for an existing table {#enable-on-existent-table}

In the example below, the items of the `mytable` table will be deleted an hour after the time set in the `created_at` column:

{% list tabs %}

- YQL

  ```yql
  ALTER TABLE `mytable` SET (TTL = Interval("PT1H") ON created_at);
  ```

- CLI

  ```bash
  $ {{ ydb-cli }} -e <endpoint> -d <database> table ttl set --column created_at --expire-after 3600 mytable
  ```


- Python

  ```python
  session.alter_table('mytable', set_ttl_settings=ydb.TtlSettings().with_date_type_column('created_at', 3600))
  ```

{% endlist %}

{% note tip %}

When setting up TTL using YQL, the `Interval` is created from a string literal in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601).

{% endnote %}

### Enabling TTL for a newly created table {#enable-for-new-table}

For a newly created table, you can pass TTL settings along with the table description:

{% list tabs %}

- YQL

  ```yql
  CREATE TABLE `mytable` (
      id Uint64,
      expire_at Timestamp,
      PRIMARY KEY (id)
  ) WITH (
      TTL = Interval("PT0S") ON expire_at
  );
  ```


- Python

  ```python
  session.create_table(
      'mytable',
      ydb.TableDescription()
      .with_column(ydb.Column('id', ydb.OptionalType(ydb.DataType.Uint64)))
      .with_column(ydb.Column('expire_at', ydb.OptionalType(ydb.DataType.Timestamp)))
      .with_primary_key('id')
      .with_ttl(ydb.TtlSettings().with_date_type_column('expire_at'))
  )
  ```

{% endlist %}

### Disabling TTL {#disable}

{% list tabs %}

- YQL

  ```yql
  ALTER TABLE `mytable` RESET (TTL);
  ```

- CLI

  ```bash
  $ {{ ydb-cli }} -e <endpoint> -d <database> table ttl drop mytable
  ```


- Python

  ```python
  session.alter_table('mytable', drop_ttl_settings=True)
  ```

{% endlist %}

### Getting TTL settings {#describe}

The current TTL settings can be obtained from the table description:

{% list tabs %}

- CLI

  ```bash
  $ {{ ydb-cli }} -e <endpoint> -d <database> scheme describe mytable
  ```


- Python

  ```python
  desc = session.describe_table('mytable')
  ttl = desc.ttl_settings
  ```

{% endlist %}
