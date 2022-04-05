---
sourcePath: ru/ydb/ydb-docs-core/ru/core/reference/ydb-sdk/recipes/auth/_includes/env.md
---
# Аутентификация при помощи переменных окружения

{% include [work in progress message](../../_includes/addition.md) %}

При использовании данного метода режим аутентификации и его параметры будут определены окружением, в котором запускается приложение, в [описанном здесь порядке](../../../auth.md#env). 

Установив одну из следующих переменных окружения, можно управлять способом аутентификации:

* `YDB_SERVICE_ACCOUNT_KEY_FILE_CREDENTIALS=<path/to/sa_key_file>` — использовать файл сервисного аккаунта в Яндекс Облаке
* `YDB_ANONYMOUS_CREDENTIALS="1"` — Использовать анонимную аутентификацию. Актуально для тестирования против докер-контейнера с {{ ydb-short-name }}
* `YDB_METADATA_CREDENTIALS="1"` — использовать сервис метаданных внутри Яндекс Облака (Яндекс функция или виртуальная машина)
* `YDB_ACCESS_TOKEN_CREDENTIALS=<access_token>` — использовать аутентификацию с токеном

Ниже приведены примеры кода аутентификации при помощи переменных окружения в разных {{ ydb-short-name }} SDK.

{% list tabs %}

- Go


  {% include [go.md](env/go.md) %}

- Java


  {% include [java.md](env/java.md) %}

{% endlist %}
