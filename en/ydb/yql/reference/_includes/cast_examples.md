---
sourcePath: en/ydb/ydb-docs-core/en/core/yql/reference/yql-docs-core-2/_includes/cast_examples.md
sourcePath: en/ydb/yql/reference/yql-docs-core-2/_includes/cast_examples.md
---
SELECT
        CAST("12345" AS Double),                -- 12345.0
        CAST(1.2345 AS Uint8),                  -- 1
        CAST(12345 AS String),                  -- "12345"
        CAST("1.2345" AS Decimal(5, 2)),        -- 1.23
        CAST("xyz" AS Uint64) IS NULL,          -- true, because it failed
        CAST(-1 AS Uint16) IS NULL, -- true, a negative integer cast to an unsigned integer
        CAST([-1, 0, 1] AS List<Uint8?>),             -- [null, 0, 1]
            --The element type is optional: the failed element is cast to null.
        CAST(["3.14", "bad", "42"] AS List<Float>),   -- [3.14, 42]
            --The element type is not optional: the failed element has been deleted.
        CAST(255 AS Uint8),                     -- 255
        CAST(256 AS Uint8) IS NULL -- true, out of range

