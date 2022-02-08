---
sourcePath: ru/ydb/ydb-docs-core/ru/core/reference/ydb-cli/profile/_includes/list-and-get.md
---
# Получение информации о профиле

Чтобы указать профиль, используйте его имя. Узнать имя профиля можно, получив список профилей.

## Получение списка профилей {#profile-list}

Получите список профилей:

```bash
{{ ydb-cli }} config profile list
```

Результат:

```text
example (active)
```

## Получение подробной информации о профиле {#profile-get}

Получите подробную информацию о профиле с именем `example`:

```bash
{{ ydb-cli }} config profile get example
```