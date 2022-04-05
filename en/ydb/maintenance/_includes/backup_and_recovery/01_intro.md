---
title: "Yandex Database (YDB) backups"
description: "This section describes supported methods for creating YDB database backups and restoring data from previously created backups. YDB lets you use the following destinations to create backups: CSV files on the file system and AWS S3-compatible storage."
sourcePath: en/ydb/ydb-docs-core/en/core/maintenance/_includes/backup_and_recovery/01_intro.md
---

# Backups

This section describes supported methods for creating YDB database backups and restoring data from previously created backups. {{ ydb-short-name }} lets you use the following destinations to create backups:
* CSV files on the file system.
* AWS S3-compatible storage.

{% note warning %}

Backups may negatively affect the database interaction indicators. Queries may take longer to execute. Before performing a database backup under load in production databases, test the process in the testing environment.

{% endnote %}