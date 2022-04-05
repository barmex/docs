---
sourcePath: ru/ydb/ydb-docs-core/ru/core/yql/reference/yql-docs-core-2/builtins/_includes/basic/staticzip.md
sourcePath: ru/ydb/yql/reference/yql-docs-core-2/builtins/_includes/basic/staticzip.md
---
## StaticZip

Поэлементно "склеивает" структуры или кортежи. Все аргументы (один и более) должны быть либо структурами с одинаковым набором полей, либо кортежами одинаковой длины.
Результататом будет соответственно структура или кортеж.
Каждый элемент результата – кортеж с соответствующими элементами из аргументов.

**Примеры:**
``` yql
$one = <|k1:1, k2:2.0|>;
$two = <|k1:3.0, k2:4|>;

-- поэлементное сложение двух структур
SELECT StaticMap(StaticZip($one, $two), ($tuple)->($tuple.0 + $tuple.1)) AS sum;
```

