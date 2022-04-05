---
sourcePath: en/ydb/ydb-docs-core/en/core/yql/reference/yql-docs-core-2/types/_includes/datatypes_primitive_string.md
sourcePath: en/ydb/yql/reference/yql-docs-core-2/types/_includes/datatypes_primitive_string.md
---
| Type | Description | Notes |
| ----- | ----- | ----- |
| `String` | A string that can contain any binary data |
| `Utf8` | Text encoded in [UTF-8](https://en.wikipedia.org/wiki/UTF-8) |
| `Json` | [JSON](https://en.wikipedia.org/wiki/JSON) represented as text | Doesn't support matching, can't be used in the primary key |
| `JsonDocument` | [JSON](https://en.wikipedia.org/wiki/JSON) in an indexed binary representation | Doesn't support matching, can't be used in the primary key |
| `Yson` | [YSON](https://yt.yandex-team.ru/docs/description/common/yson.html) in a textual or binary representation. | Doesn't support matching, can't be used in the primary key |
| `Uuid` | Universally unique identifier [UUID](https://tools.ietf.org/html/rfc4122) | Not supported for table columns |

{% note info "Cell size restrictions" %}

The maximum value size for a non-key column cell with any string data type is 8 MB.

{% endnote %}

Unlike the `JSON` data type that stores the original text representation passed by the user, `JsonDocument` uses an indexed binary representation. An important difference from the point of view of semantics is that `JsonDocument` doesn't preserve formatting, the order of keys in objects, or their duplicates.

Thanks to the indexed view, `JsonDocument` lets you bypass the document model using `JsonPath` without the need to parse the full content. This helps efficiently perform operations from the [JSON API](../../builtins/json.md), reducing delays and cost of user queries. Execution of `JsonDocument` queries can be up to several times more efficient depending on the type of load.

Due to the added redundancy, `JsonDocument` is less effective in storage. The additional storage overhead depends on the specific content, but is 20-30% of the original volume on average. Saving data in `JsonDocument` format requires additional conversion from the textual representation, which makes writing it less efficient. However, for most read-intensive scenarios that involve processing data from JSON, this data type is preferred and recommended.

{% note warning %}

To store numbers (JSON Number) in `JsonDocument`, as well as for arithmetic operations on them in the [JSON API](../../builtins/json.md), the [Double](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) type is used. Precision might be lost when non-standard representations of numbers are used in the source JSON document.

{% endnote %}

