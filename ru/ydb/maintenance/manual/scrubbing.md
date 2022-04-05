---
sourcePath: ru/ydb/ydb-docs-core/ru/core/maintenance/manual/scrubbing.md
---
# Включение/выключение Scrubbing

Настройки Scrub позволяют регулировать интервал времени, который проходит от начала предыдущего цикла скраббинга диска до начала следующего, а также максимальное число дисков, которые могут скрабиться одновременно. Значение по умолчанию — 1 месяц.
`$ kikimr admin bs config invoke --proto 'Command { UpdateSettings { ScrubPeriodicitySeconds: 86400 MaxScrubbedDisksAtOnce: 1 } }'`

В случае, если ScrubPeriodicitySeconds равен 0, то Scrubbing выключен.
