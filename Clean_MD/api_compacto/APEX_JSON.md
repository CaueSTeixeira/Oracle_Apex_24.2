<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_JSON (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_JSON

This package includes utilities that parse and generate JSON.

---

## APEX_JSON Overview and Examples

To read from a string that contains JSON data, first use `parse()` to
convert the string to an internal format. Then use the
`get_%` routines (for example,
`get_varchar2()`, `get_number()`, ...)
to access the data and `find_paths_like()` to search.

Alternatively, use `to_xmltype()` to convert a JSON string to an xmltype.

This package also contains procedures to generate JSON-formatted output. Use the overloaded `open_%()`, `close_%()` and `write()` procedures for writing to the SYS.HTP buffer. To write to a temporary CLOB instead, use `initialize_clob_output()`, `get_clob_output()`, and `free_output()` for managing the output buffer.

---

## Constants and Data Types

Parser Interface

The following constants are used for the parser interface:

```sql
subtype t_kind is binary_integer range 1 .. 8;
c_null     constant t_kind := 1;
c_true     constant t_kind := 2;
c_false    constant t_kind := 3;
c_number   constant t_kind := 4;
c_varchar2 constant t_kind := 5;
c_object   constant t_kind := 6;
c_array    constant t_kind := 7;
c_clob     constant t_kind := 8;
```

Storage for JSON Data

JSON data is stored in an index by varchar2 table. The JSON values are stored as records. The discriminator "kind" determines whether the value is null, true, false, a number, a varchar2, a clob, an object or an array. It depends on "kind" which record fields are used and how. If not explicitly mentioned below, the other record fields' values are undefined:

\* c_null: -

\* c_true: -

\* c_false: -

\* c_number: number_value contains the number value

\* c_varchar2: varchar2_value contains the varchar2 value

\* c_clob: clob_value contains the clob

\* c_object: object_members contains the names of the object's members

\* c_array: number_value contains the array length

```sql
type t_value is record (
   kind           t_kind,
   number_value   number,
   varchar2_value varchar2(32767),
   clob_value clob,
   object_members apex_t_varchar2 );
type t_values is table of t_value index by varchar2(32767);
```

Default Format for Dates

```sql
c_date_iso8601 constant varchar2(30) := 'yyyy-mm-dd"T"hh24:mi:ss"Z"';
```

Default JSON Values Table

```sql
g_values t_values;
```

Errors Thrown for PARSE()

```sql
e_parse_error     exception;
pragma exception_init(e_parse_error, -20987);
```

---

## CLOSE_ALL Procedure

This procedure closes all objects and arrays up to the outermost nesting level.

Syntax

```sql
APEX_JSON.CLOSE_ALL;
```

Parameters

None.

---

## CLOSE_ARRAY Procedure

This procedure writes a close bracket symbol as follows:

```sql
]
```

Syntax

```sql
APEX_JSON.CLOSE_ARRAY ();
```

Parameters

None.

---

## CLOSE_OBJECT Procedure

This procedure writes a close curly bracket symbol as follows:

```sql
}
```

Syntax

```sql
APEX_JSON.CLOSE_OBJECT ();
```

Parameters

None.

---

## DOES_EXIST Function

This function determines whether the given path points to an existing value.

Syntax

```sql
APEX_JSON.DOES_EXIST (
   p_path             IN VARCHAR2,
   p0                 IN VARCHAR2 DEFAULT NULL,
   p1                 IN VARCHAR2 DEFAULT NULL,
   p2                 IN VARCHAR2 DEFAULT NULL,
   p3                 IN VARCHAR2 DEFAULT NULL,
   p4                 IN VARCHAR2 DEFAULT NULL,
   p_values           IN t_values DEFAULT g_values )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each %N in `p_path` is replaced by `pN` and every i-th %s or %d is replaced by the `p[i-1]`. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns

| Return | Description |
| --- | --- |
| `TRUE` | Given path points to an existing value. |
| `FALSE` | Given path does not point to an existing value |

---

## FIND_PATHS_LIKE Function

This function returns paths into `p_values` that match a given pattern.

Syntax

```sql
APEX_JSON.FIND_PATHS_LIKE (
    p_return_path      IN VARCHAR2,
    p_subpath          IN VARCHAR2 DEFAULT NULL,
    p_value            IN VARCHAR2 DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
RETURN apex_t_varchar2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_return_path` | Search pattern for the return path.. |
| `p_subpath` | (Optional) Search pattern under `p_return_path`. |
| `p_value` | (Optional) Search pattern for value. |
| `p_values` | Parsed JSON members. Default is `g_values`. |

Returns/Raised Errors

| Return/Error | Description |
| --- | --- |
| `apex_t_varchar2` | Table of paths that match the pattern. |
| `VALUE_ERROR` | Raises this error if `p_values(p_path` is not an array or object. |

---

## FLUSH Procedure

This procedure flushes pending changes. Note that close procedures automatically flush.

Syntax

```sql
APEX_JSON.FLUSH
```

Parameters

None.

---

## FREE_OUTPUT Procedure

Frees output resources. Call this procedure after process if you are using `INITIALIZE_CLOB_OUTPUT` to write to a temporary `CLOB`.

Syntax

```sql
APEX_JSON.FREE_OUTPUT;
```

---

## GET_BOOLEAN Function

This function returns a boolean member value.

Syntax

```sql
APEX_JSON.GET_BOOLEAN (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_default          IN BOOLEAN  DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each %N in `p_path` is replaced by `pN` and every i-th %s or %d is replaced by the `p[i-1]`. |
| `p_default` | The default value if the member does not exist. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns

| Return | Description |
| --- | --- |
| `TRUE` | Value at the given path position. |
| `FALSE` | Value at the given path position. |
| `NULL` | Value at the given path position. |
| `VALUE_ERROR` | Raises this error if `p_values(p_path)` is not boolean. |

---

## GET_CLOB Function

This function returns clob member value. This function auto-converts `varchar2`, boolean, and number values.

Syntax

```sql
GET_CLOB (
    p_path    IN VARCHAR2,
    p0        IN VARCHAR2 DEFAULT NULL,
    p1        IN VARCHAR2 DEFAULT NULL,
    p2        IN VARCHAR2 DEFAULT NULL,
    p3        IN VARCHAR2 DEFAULT NULL,
    p4        IN VARCHAR2 DEFAULT NULL,
    p_default IN CLOB     DEFAULT NULL,
    p_values  in t_values DEFAULT g_values )
RETURN CLOB
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_values` | Parsed JSON members. defaults to `g_values`. |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each `%N` in `p_path` is replaced with `pN` and every `i-th %s` or `%d` is replaced with `p[i-1]`. |
| `p_default` | Default value if the member does not exist. |

Returns/Raised Errors

| Return/Error | Description |
| --- | --- |
| `a clob` | Value at the given path position. |
| `VALUE_ERROR` | If `p_values(p_path)` is an array or an object. |

---

## GET_CLOB_OUTPUT Function

Returns the temporary `CLOB` that you created with `INITIALIZE_CLOB_OUTPUT`.

Syntax

```sql
APEX_JSON.GET_CLOB_OUTPUT (
    p_free  IN BOOLEAN  DEFAULT FALSE )
    RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_free` | If `true`, frees output resources. Defaults to false. |

---

## GET_COUNT Function

This function returns the number of array elements or object members.

Syntax

```sql
APEX_JSON.GET_COUNT (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each %N in `p_path` is replaced by `pN` and every i-th %s or %d is replaced by the `p[i-1]`. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns/Raised Errors

| Return/Error | Description |
| --- | --- |
| `NUMBER` | The number of array elements or object members or null if the array or object could not be found |
| `VALUE_ERROR` | Raises this error if `p_values(p_path)` is not an array or object. |

---

## GET_DATE Function

This function returns a date member value.

Syntax

```sql
APEX_JSON.GET_DATE (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_default          IN DATE     DEFAULT NULL,
    p_format           IN VARCHAR2 DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
RETURN DATE;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each %N in `p_path` is replaced by `pN` and every i-th %s or %d is replaced by the `p[i-1]`. |
| `p_default` | The default value if the member does not exist. |
| `p_format` | The date format mask. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns/Raised Errors

| Return | Description |
| --- | --- |
| `DATE` | Returns the date. |
| `VALUE_ERROR` | Raises this error if `p_values(p_path)` is not a date. |

---

## GET_MEMBERS Function

This function returns the table of `OBJECT_MEMBERS` names for an object.

Syntax

```sql
APEX_JSON.GET_MEMBERS (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
RETURN APEX_T_VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each `%N` in `p_path` is replaced by `pN` and every `i-th%` or `%d` is replaced by the `p[i-1]`. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns/Raised Errors

| Return/Error | Description |
| --- | --- |
| `OBJECT_MEMBERS` | The `OBJECT_MEMBERS` of the object or null if the object could not be found. |
| `VALUE_ERROR` | Raises this error if `p_values(p_path)` is not an array or object. |

---

## GET_NUMBER Function

This function returns a numeric member value.

Syntax

```sql
APEX_JSON.GET_NUMBER (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_default          IN BOOLEAN  DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each `%N` in `p_path` is replaced by `pN` and every `i-th%` or `%d` is replaced by the `p[i-1]`. |
| `p_default` | The default value if the member does not exist. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns and Raised Errors

| Return | Description |
| --- | --- |
| `NUMBER` | The value at the given path position. |
| `VALUE_ERROR` | Raises this error if `p_values(p_path)` is not a number. |

---

## GET_SDO_GEOMETRY Function

This function returns SDO_GEOMETRY member value from a GeoJSON member. This function supports only two-dimensional geometry objects.

Note:

This function is only available if SDO_GEOMETRY (Oracle Locator) is installed in the database.

Syntax

```sql
APEX_JSON.GET_SDO_GEOMETRY FUNCTION (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2  DEFAULT NULL,
    p1                 IN VARCHAR2  DEFAULT NULL,
    p2                 IN VARCHAR2  DEFAULT NULL,
    p3                 IN VARCHAR2  DEFAULT NULL,
    p4                 IN VARCHAR2  DEFAULT NULL,
    p_srid             IN NUMBER    DEFAULT 4326,
    p_values           IN t_values  DEFAULT g_values )
    RETURN mdsys.sdo_geometry;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_values` | Parsed JSON members. Defaults to `g_values`. |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each `%N` in `p_path` is replaced by `pN` and every `i-th %s` or `%d` is replaced by the `p[i-1]`. |
| `p_srid` | Coordinate system (SRID) to return the SDO_GEOMETRY in. |

Returns

| Return | Description |
| --- | --- |
| a geometry | Value at the given path position. |

Errors Raised

| Raise | Description |
| --- | --- |
| `VALUE_ERROR` | If `p_values(p_path)` is not a GeoJSON object. |

---

## GET_T_NUMBER Function

This function returns the numeric attributes of an array.

Syntax

```sql
APEX_JSON.GET_T_NUMBER (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
    RETURN apex_t_number;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each `%N` in `p_path` is replaced by `pN` and every `i-th%` or `%d` is replaced by the `p[i-1]`. |
| `p_values` | Parsed JSON members. Default `p_values`. |

Returns

Array member values if the referenced `t_value` is an array. An array with just the referenced value if its type can be converted to a number.

| Return | Description |
| --- | --- |
| `VALUE_ERROR` | On conversion errors. |

---

## GET_T_VARCHAR2 Function

This function returns the varchar2 attributes of an array.

Syntax

```sql
APEX_JSON.GET_T_VARCHAR2 (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
    RETURN apex_t_varchar2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each %N in `p_path` is replaced by `pN` and every `i-th%` or `%d` is replaced by the `p[i-1]`. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns

Array member values if the referenced `t_value` is an array. An array with just the referenced value if its type can be converted to a varchar2.

Raises

| Return | Description |
| --- | --- |
| `VALUE_ERROR` | On conversion errors. |

---

## GET_VALUE Function

This function returns the t_value.

Syntax

```sql
APEX_JSON.GET_VALUE (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
RETURN t_value;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each `%N` in `p_path` is replaced by `pN` and every `i-th%` or `%d` is replaced by the `p[i-1]`. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns/Raised Errors

| Return | Description |
| --- | --- |
| `t_value` | The `t_value` at the given path position. The record attributes are null if no data is found. |
| `VALUE_ERROR` | Raises this error if `p_values(p_path)` is not an array or object. |

---

## GET_VALUE_KIND Function

This function returns the kind of the value at a path position.

Syntax

```sql
APEX_JSON.GET_VALUE_KIND (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
    RETURN t_kind;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_values` | Parsed JSON members. Defaults to `g_values`. |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each `%N` in `p_path` is replaced by `pN` and every `i-th %s` or `%d` is replaced by the `p[i-1]`. |

Table 37-1 Returns

| Return | Description |
| --- | --- |
| `t_kind` | The `t_kind` of the value at the given path position. Returns NULL if no data is found. |

---

## GET_VARCHAR2 Function

This function returns a varchar2 member value. This function converts boolean and number values to varchar2 values.

Syntax

```sql
APEX_JSON.GET_VARCHAR2 (
    p_path             IN VARCHAR2,
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_default          IN BOOLEAN  DEFAULT NULL,
    p_values           IN t_values DEFAULT g_values )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_path` | Index into `p_values`. |
| `p[0-4]` | Each %N in `p_path` is replaced by `pN` and every i-th %s or %d is replaced by the `p[i-1]`. |
| `p_default` | The default value if the member does not exist. |
| `p_values` | Parsed JSON members. The default is `g_values`. |

Returns and Raised Errors

| Return/Error | Description |
| --- | --- |
| `VARCHAR2` | This is the value at the given path position. |
| `VALUE_ERROR` | Raises this error if `p_values(p_path)` is not an array or object. |

---

## INITIALIZE_CLOB_OUTPUT Procedure

This procedure initializes the output interface to write to a temporary CLOB. The default is to write to `SYS.HTP`. If using CLOB output, call `FREE_OUTPUT()` at the end to free the `CLOB`.

Syntax

```sql
APEX_JSON.INITIALIZE_CLOB_OUTPUT (
    p_dur         IN PLS_INTEGER DEFAULT sys.dbms_lob.call,
    p_cache       IN BOOLEAN     DEFAULT TRUE,
    p_indent      IN PLS_INTEGER DEFAULT NULL,
    p_preserve    IN BOOLEAN     DEFAULT FALSE )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_dur` | Duration of the temporary `CLOB`. this can be `DBMS_LOB.SESSION` or `DBMS_LOB.CALL` (the default). |
| `p_cache` | Specifies if the lob should be read into buffer cache or not. |
| `p_indent` | Indent level. Defaults to 2 if debug is turned on, 0 otherwise. |
| `p_preserve` | Whether to preserve the currently active output object.  After calling `FREE_OUTPUT`, subsequent write calls will be executed on the preserved output. Defaults to `FALSE`.  If HTP output has already been initialized and a CLOB needs to be created, use `p_preserve => true`. After `FREE_OUTPUT`, subsequent output will be directed to the original HTP output again.  If `p_preserve` is `true`, you must call `FREE_OUTPUT` after JSON processing. |

---

## INITIALIZE_OUTPUT Procedure

This procedure initializes the output interface. You only have to call this procedure if you want to modify the parameters below. Initially, output is already configured with the defaults mentioned in the parameter table.

Syntax

```sql
APEX_JSON.INITIALIZE_OUTPUT (
    p_http_header     IN BOOLEAN     DEFAULT TRUE,
    p_http_cache      IN BOOLEAN     DEFAULT FALSE,
    p_http_cache_etag IN VARCHAR2    DEFAULT NULL,
    p_indent          IN PLS_INTEGER DEFAULT NULL )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_http_header` | If TRUE (default), writes an application/JSON mime type header. |
| `p_http_cache` | This parameter is only relevant if `p_http_header` is TRUE. If TRUE, writes Cache-Control: max-age=315360000. If FALSE (the default), writes Cache-Control: no-cache. Otherwise, does not write Cache-Control. |
| `http_cache_etag` | If not null, writes an `etag` header. This parameter is only used if `P_HTTP_CACHE` is true. |
| `p_indent` | Indent level. Defaults to 2, if debug is turned on, otherwise defaults to 0. |

---

## OPEN_ARRAY Procedure

This procedure writes an open bracket symbol as follows:

```sql
[
```

Syntax

```sql
APEX_JSON.OPEN_ARRAY (
    p_name     IN VARCHAR2 DEFAULT NULL )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | If not null, write an object attribute name and colon before the opening bracket. |

---

## OPEN_OBJECT Procedure

This procedure writes an open curly bracket symbol as follows:

```sql
{
```

Syntax

```sql
APEX_JSON.OPEN_OBJECT (
    p_name     IN VARCHAR2 DEFAULT NULL )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | If not null, write an object attribute name and colon before the opening brace. |

---

## PARSE Procedure Signature 1

This procedure parses a JSON-formatted `VARCHAR2` or `CLOB` and puts the members into `p_values`.

Syntax

```sql
APEX_JSON.PARSE (
    p_values   IN OUT NOCOPY   t_values,
    p_source   IN VARCHAR2,
    p_strict   IN BOOLEAN      DEFAULT TRUE );

APEX_JSON.PARSE (
    p_values   IN OUT NOCOPY   t_values,
    p_source   IN CLOB,
    p_strict   IN BOOLEAN      DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_values` | An index by `VARCHAR2` result array which contains the JSON members and values. The default is `g_values`. |
| `p_source` | The JSON source (`VARCHAR2` or `CLOB`) |
| `p_strict` | If `TRUE` (default), enforce strict JSON rules |

---

## PARSE Procedure Signature 2

This procedure parses a JSON-formatted `varchar2` or `clob` and puts the members into the package global `g_values`. This simplified API works similar to the `parse()` procedure for signature 1, but saves the developer from declaring a local variable for parsed JSON data and passing it to each JSON API call.

Syntax

```sql
APEX_JSON.PARSE (
    p_source    IN VARCHAR2,
    p_strict    IN BOOLEAN  DEFAULT TRUE );

APEX_JSON.PARSE (
    p_source    IN CLOB,
    p_strict    IN BOOLEAN  DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_source` | The JSON source (`VARCHAR2` or `CLOB`). |
| `p_strict` | If `TRUE` (default), enforce strict JSON rules. |

---

## STRINGIFY Function Signature 1

This function converts a string to an escaped JSON value.

Syntax

```sql
APEX_JSON.STRINGIFY (
    p_value  IN VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The string to be converted. |

Returns

| Return | Description |
| --- | --- |
| `VARCHAR2` | The converted and escaped JSON value. |

---

## STRINGIFY Function Signature 2

This function converts a number to an escaped JSON value.

Syntax

```sql
APEX_JSON.STRINGIFY (
    p_value  IN NUMBER )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The number to be converted. |

Returns

| Return | Description |
| --- | --- |
| `VARCHAR2` | The converted and escaped JSON value. |

---

## STRINGIFY Function Signature 3

This function converts a date to an escaped JSON value.

Syntax

```sql
APEX_JSON.STRINGIFY (
    p_value  IN DATE,
    p_format IN VARCHAR2 DEFAULT c_date_iso8601 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The date value to be converted. |

Returns

| Return | Description |
| --- | --- |
| `VARCHAR2` | The converted and escaped JSON value. |

---

## STRINGIFY Function Signature 4

This function converts a boolean value to an escaped JSON value.

Syntax

```sql
APEX_JSON.STRINGIFY (
    p_value  IN BOOLEAN )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The boolean value to be converted. |

Returns

| Return | Description |
| --- | --- |
| `VARCHAR2` | The converted and escaped JSON value. |

---

## STRINGIFY Function Signature 5

This function converts `p_value` to a GeoJSON value.

Note:

This signature is only available if SDO_GEOMETRY (Oracle Locator) is installed in the database.

Syntax

```sql
APEX_JSON.STRINGIFY (
    p_value IN mdsys.sdo_geometry )
    RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The sdo_geometry value to be converted. |

Returns

| Return | Description |
| --- | --- |
| `CLOB` | The GeoJSON value. |

---

## TO_MEMBER_NAME Function

This function converts the given string to a JSON member name, usable for accessing values via the `get_%` functions. Unless member names are simple identifiers (`A-Z,0-9, "_"`), they need to be quoted.

Syntax

```sql
FUNCTION TO_MEMBER_NAME (
   p_string IN VARCHAR2 )
   RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_string` | The raw member name. |

Returns

A valid member name for `get_%` functions.

---

## TO_XMLTYPE Function

This procedure parses a JSON-formatted `varchar2` or `CLOB` and converts it to an xmltype.

Syntax

```sql
APEX_JSON.TO_XMLTYPE (
    p_source   IN VARCHAR2,
    p_strict   IN BOOLEAN DEFAULT TRUE )
RETURN sys.xmltype;

APEX_JSON.TO_XMLTYPE (
    p_source   IN CLOB,
    p_strict   IN BOOLEAN DEFAULT TRUE )
RETURN sys.xmltype;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_source` | The JSON source (`VARCHAR2` or `CLOB`) |
| `p_strict` | If TRUE (default), enforce strict JSON rules |

Returns

| Return | Description |
| --- | --- |
| `sys.xmltype` | An `xmltype` representation of the JSON data. |

---

## TO_XMLTYPE_SQL Function

This function parses a JSON-formatted `varchar2` or `CLOB` and converts it to an xmltype. This function overload has the `p_strict` parameter as `VARCHAR2` in order to allow invoking from within a SQL query and having JSON parsing in LAX mode.

Syntax

```sql
APEX_JSON.TO_XMLTYPE_SQL (
    p_source   IN VARCHAR2,
    p_strict   IN VARCHAR2 DEFAULT 'Y' )
RETURN sys.xmltype;

APEX_JSON.TO_XMLTYPE_SQL (
    p_source   IN CLOB,
    p_strict   IN VARCHAR2 DEFAULT 'Y' )
RETURN sys.xmltype;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_source` | The JSON source (`VARCHAR2` or `CLOB`) |
| `p_strict` | If Y (default), enforce strict JSON rules |

Returns

An xmltype representation of the json data

---

## WRITE Procedure Signature 1

This procedure writes an array attribute of type `VARCHAR2`.

Syntax

```sql
APEX_JSON.WRITE (
    p_value    IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The value to be written. |

---

## WRITE Procedure Signature 2

This procedure writes an array attribute of type `clob`.

Syntax

```sql
APEX_JSON.WRITE (
    p_value    IN CLOB );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The value to be written. |

---

## WRITE Procedure Signature 3

This procedure writes an array attribute of type `NUMBER`.

Syntax

```sql
APEX_JSON.WRITE (
    p_value    IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The value to be written. |

---

## WRITE Procedure Signature 4

This procedure writes an array attribute. of type date.

Syntax

```sql
APEX_JSON.WRITE (
    p_value    IN DATE,
    p_format   IN VARCHAR2 DEFAULT c_date_iso8601 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The value to be written. |
| `p_format` | The date format mask (default `c_date_iso8601`). |

---

## WRITE Procedure Signature 5

This procedure writes an array attribute of type `boolean`.

Syntax

```sql
APEX_JSON.WRITE (
    p_value    IN BOOLEAN );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The value to be written. |

---

## WRITE Procedure Signature 6

This procedure writes an array attribute of type `sys.xmltype`. The procedure uses a XSL transformation to generate JSON. To determine the JSON type of values, it uses the following rules:

* If the value is empty, it generates a `NULL` value.
* If upper(value) is `TRUE`, it generates a boolean true value.
* If upper(value) is `FALSE`, it generates a boolean false value.
* If the `XPath` number function returns `TRUE`, it emits the value as is. Otherwise, it enquotes the value (that is, treats it as a JSON string).

Syntax

```sql
APEX_JSON.WRITE (
    p_value    IN sys.xmltype );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The value to be written. |

---

## WRITE Procedure Signature 7

This procedure writes an array with all rows that the cursor returns. Each row is a separate object. If the query contains object type, collection, or cursor columns, the procedure uses `write(xmltype)` to generate JSON. Otherwise, it uses `DBMS_SQL` to fetch rows and the`write()` procedures for the appropriate column data types for output. If the column type is `varchar2` and the uppercase value is `'TRUE'` or `'FALSE'`, it generates boolean values.

Syntax

```sql
APEX_JSON.WRITE (
    p_cursor      IN OUT NOCOPY sys_refcursor );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_cursor` | The cursor. |

---

## WRITE Procedure Signature 8

This procedure writes array attribute of type SDO_GEOMETRY.

Note:

This signature is only available if SDO_GEOMETRY (Oracle Locator) is installed in the database.

Syntax

```sql
APEX_JSON.WRITE (
    p_value       IN mdsys.sdo_geometry );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The value to be written. |

---

## WRITE Procedure Signature 9

This procedure writes an object attribute of type `VARCHAR2`.

Syntax

```sql
APEX_JSON.WRITE (
    p_name        IN VARCHAR2,
    p_value       IN VARCHAR2,
    p_write_null  IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_value` | The attribute value to be written. |
| `p_write_null` | If `TRUE`, write `NULL` values. If `FALSE` (default), do not write NULLs. |

---

## WRITE Procedure Signature 10

This procedure writes an object attribute of type `CLOB`.

Syntax

```sql
APEX_JSON.WRITE (
    p_name         IN VARCHAR2,
    p_value        IN CLOB,
    p_write_null   IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_value` | The attribute value to be written. |
| `p_write_null` | If `TRUE`, write `NULL` values. If `FALSE` (the default), do not write `NULL`s. |

---

## WRITE Procedure Signature 11

This procedure writes an object attribute of type `NUMBER`.

Syntax

```sql
APEX_JSON.WRITE (
    p_name         IN VARCHAR2,
    p_value        IN NUMBER,
    p_write_null   IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_value` | The attribute value to be written. |
| `p_write_null` | If TRUE, write `NULL` values. If false (the default), do not write `NULL`s. |

---

## WRITE Procedure Signature 12

This procedure writes an object attribute of type `date`.

Syntax

```sql
APEX_JSON.WRITE (
    p_name         IN VARCHAR2,
    p_value        IN DATE,
    p_format       IN VARCHAR2 DEFAULT c_date_iso8601,
    p_write_null   IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_value` | The attribute value to be written. |
| `p_format` | The date format mask (default `apex_json.c_date_iso8601`). |
| `p_write_null` | If TRUE, write `NULL` values. If FALSE (default), do not write `NULL`. |

---

## WRITE Procedure Signature 13

This procedure writes an object attribute of type `boolean`.

Syntax

```sql
APEX_JSON.WRITE (
    p_name         IN VARCHAR2,
    p_value        IN BOOLEAN,
    p_write_null   IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_value` | The attribute value to be written. |
| `p_write_null` | If TRUE, write `NULL` values. If FALSE (default), do not write `NULL`. |

---

## WRITE Procedure Signature 14

This procedure writes an attribute where the value is an array that contains all rows that the cursor returns. Each row is a separate object.

If the query contains object type, collection, or cursor columns, the procedure uses `write(p_name,<xmltype>)`. See WRITE Procedure Signature 15. Otherwise, it uses `DBMS_SQL` to fetch rows and the `write()` procedures for the appropriate column data types for output. If the column type is `varchar2` and the uppercase value is `'TRUE'` or `'FALSE'`, it generates boolean values.

Syntax

```sql
APEX_JSON.WRITE (
    p_name        IN VARCHAR2,
    p_cursor      IN OUT NOCOPY sys_refcursor );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_cursor` | The cursor. |

---

## WRITE Procedure Signature 15

This procedure writes an array attribute of type `sys.xmltype`. The procedure uses a XSL transformation to generate JSON. To determine the JSON type of values, it uses the following rules:

* If the value is empty, it generates a `NULL` value.
* If upper(value) is `TRUE`, it generates a boolean true value.
* If upper(value) is `FALSE`, it generates a boolean false value.
* If the `XPath` number function returns true, it emits the value as is. Otherwise, it enquotes the value (that is, treats it as a JSON string).

Syntax

```sql
APEX_JSON.WRITE (
    p_name         IN VARCHAR2,
    p_value        IN sys.xmltype,
    p_write_null   IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_value` | The value to be written. The XML is converted to JSON |
| `p_write_null` | If TRUE, write `NULL` values. If FALSE (default), do not write `NULL`s. |

---

## WRITE Procedure Signature 16

This procedure writes parts of a parsed `APEX_JSON.t_values` table.

Syntax

```sql
APEX_JSON.WRITE (
    p_values           IN t_values,
    p_path             IN VARCHAR2 DEFAULT '.',
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_values` | The parsed JSON members. |
| `p_path` | The index into `p_values`. |
| `p[0-4]` | Each `%N` in `p_path` will be replaced by `pN` and every `i-th %s` or `%d` is replaced by `p[i-1]`. |

---

## WRITE Procedure Signature 17

This procedure writes parts of a parsed `APEX_JSON.t_values` table as an object member attribute.

Syntax

```sql
APEX_JSON.WRITE (
    p_name             IN VARCHAR2,
    p_values           IN t_values,
    p_path             IN VARCHAR2 DEFAULT '.',
    p0                 IN VARCHAR2 DEFAULT NULL,
    p1                 IN VARCHAR2 DEFAULT NULL,
    p2                 IN VARCHAR2 DEFAULT NULL,
    p3                 IN VARCHAR2 DEFAULT NULL,
    p4                 IN VARCHAR2 DEFAULT NULL,
    p_write_null       IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_values` | The parsed JSON members. |
| `p_path` | The index into `p_values`. |
| `p[0-4]` | Each %N in `p_path` will be replaced by `pN` and every i-th %s or %d is replaced by p[i-1]. |
| `p_write_null` | If true, write `NULL` values. If false (the default), do not write `NULL`s. |

---

## WRITE Procedure Signature 18

This procedure writes an array attribute of type `VARCHAR2`.

Syntax

```sql
APEX_JSON.WRITE (
      p_name        IN VARCHAR2,
      p_values      IN apex_t_varchar2,
      p_write_null  IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_values` | The `VARCHAR2` array values to be written. |
| `p_write_null` | If true, write an empty array. If false (the default), do not write an empty array. |

---

## WRITE Procedure Signature 19

This procedure writes an array attribute of type `NUMBER` .

Syntax

```sql
APEX_JSON.WRITE (
   p_name        IN VARCHAR2,
   p_values      IN apex_t_number,
   p_write_null  IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_values` | The `NUMBER` array values to be written. |
| `p_write_null` | If true, write an empty array. If false (the default), do not write an empty array. |

---

## WRITE Procedure Signature 20

This procedure writes a BLOB object attribute. The value will be Base64-encoded.

Syntax

```sql
APEX_JSON.WRITE (
   p_name        IN VARCHAR2
   p_value       IN BLOB,
   p_write_null  IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_values` | The attribute value to be written. |
| `p_write_null` | If `TRUE`, write an empty array. If `FALSE` (default), do not write an empty array. |

---

## WRITE Procedure Signature 21

This procedure writes an object attribute.

Note:

This signature is only available if SDO_GEOMETRY (Oracle Locator) is installed in the database.

Syntax

```sql
APEX_JSON.WRITE (
    p_name        IN VARCHAR2,
    p_value       IN mdsys.sdo_geometry,
    p_write_null  IN BOOLEAN DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_value` | The attribute value to be written. |
| `p_write_null` | If `TRUE`, write null values. If `FALSE` (the default), do not write nulls. |

---

## WRITE_CONTEXT Procedure

This procedure writes an array with all rows that the context handle returns. Each row is a separate object.

If the query contains object type, collection or cursor columns, an error is raised. If the column is `VARCHAR2` and the uppercase value is 'TRUE' or 'FALSE', boolean values are generated.

Syntax

```sql
PROCEDURE WRITE_CONTEXT (
   p_name        IN VARCHAR2
   p_context     IN apex_exec.t_context,
   p_write_null  IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The attribute name. |
| `p_context` | The context handle from an `APEX_EXEC.OPEN_QUERY_CONTEXT` call. |
| `p_write_null` | Whether to write (TRUE) or omit (FALSE) NULL values. |