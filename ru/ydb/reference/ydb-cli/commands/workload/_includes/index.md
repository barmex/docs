---
sourcePath: ru/ydb/ydb-docs-core/ru/core/reference/ydb-cli/commands/workload/_includes/index.md
---
# Нагрузочное тестирование

С помощью команды `workload` вы можете запустить различные виды нагрузки для вашей БД.

Общий вид команды:

```bash
{{ ydb-cli }} [global options...] workload [subcommands...]
```

* `global options` — [глобальные параметры](../../../commands/global-options.md).
* `subcommands` — [подкоманды](#subcomands).

Посмотрите описание команды для запуска нагрузки:

```bash
{{ ydb-cli }} workload --help
```

## Доступные подкоманды {#subcommands}

В данный момент поддерживаются следующие виды нагрузочных тестов:
* [Stock](../stock.md) - симулятор склада интернет-магазина.